
# package

<!-- badges: start -->
<!-- badges: end -->

The goal of package is to ...

## Installation

You can install the development version of package from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("science-collective/package")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(package)
## basic example code
```

# pubmedciteR
An R package for easier citation of PubMed articles in restricted virtual environments


## Aim

The aim of this package is to make life easier for anyone writing research articles within a restricted virtual environment, e.g. using `Rmarkdown` with the `rticles`-package on a remote server where the outside internet cannot be accessed and citation data cannot be downloaded. Hopefully, this project can provide an alternative to manually typing in every bibliography entry. I may even be preferential to manually downloading and copy/pasting bibtex entries when working on your local computer.

## Overview of planned features:

- Create functions to enable easy downloading of PubMed's annually updated baseline files and creating a local, easy-to-work-with copy of the citation data:
  - Download and and convert the gz-zipped xml files found at https://ftp.ncbi.nlm.nih.gov/pubmed/baseline/ into a data frame-like object (perhaps a keyed `data.table`) and save it locally.
    - The user's system admin must then be persuaded to either run these functions and download the baseline files and make the output from the scripts available within the restricted virtual environment. Or, more likely, simply download the output file(s) created by the package maintainers or the user.
- Create functions to quickly and easily search the output data frame for citations and add them to a bibliography.


## To do's & thoughts


### Should be fairly straight-forward from here on, but optimizations for speed and reduces memory footprint of the output would be tremendously helpful:

- ftp_to_dt.R: 
1. Convert `tibble` to a `data.table` for faster wrangling?
2. Create string variables corresponding to elements of a bibtex entry
3. Iterate over all .gz files in the ftp folder
4. Bind rows of all files into a single data frame (or maybe several)
5. Save this data frame to disk. This file will not be part of the package due to size restrictions. To spare users from having to spend days/months running this script themselves, it could be uploaded and made available for download from another source (google drive or better alternatives?)

- row_to_bibtex.R:
6. Create function to write/append a specific row from the data frame to a bibliography-file as a bibtex entry with `sink()`:

7. User opens the data frame, runs the above function on row(s) specified by ordinary filtering operations and writes bibliography on an as-needed basis.


### Issues:

- There's ~1100 files on the ftp server so the current implementation would take 3-4 months to finish iterating through them on a standard laptop.
- The output will likely be too large to fit comfortably in memory if all files are row-binded together.

### Solutions:

- The current method of unnest'ing each layer of the nested lists is far from efficient and takes way too much time. A much more efficient way would be to define each of the final columns by extracting the contents of the list directly, instead of unnesting and name_repair'ing millions of lists in lists. Even better would be to directly extract the end/leaf items from the xml-file using a more precise XPath query, if that is possible.
  - Some big brain on StackOverflow could probably come up with something very good here, since the data is openly available. Might be worth looking into posting a question there (even though it takes a potentially fun challenge away from us)
- Hopefully, the files on the ftp server are numbered in order of the year of publication (they appear to be). We may need to divide the citation data into several separate files, based on publication year to work around the size limits (e.g. a separate file for each year). This should still be relatively easy for the end-user to work with, e.g. by adding a publication-year-argument to the row_to_bibtex(), which then reads the corresponding data frame.
