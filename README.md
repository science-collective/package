

# package:

This repository is intended as a tool to supplement the "Issues"-list on GitHub and help the package group share and discuss thoughts related to our work, as set out in issue 6 (https://github.com/science-collective/admin/issues/6)

# Brief description of folder and file contents

TODO: As project evolves, add brief description of what is inside the data, doc and R folders.

The following folders contain:

- `doc/reflections/`: logs of our experiences working on and collaborating in this project.


# Installing project R package dependencies

If dependencies have been managed by using `usethis::use_package("packagename")`
through the `DESCRIPTION` file, installing dependencies is as easy as opening the
`package.Rproj` file and running this command in the console:

    # install.packages("remotes")
    remotes::install_deps()

You'll need to have remotes installed for this to work.

# Resource

For more information on this folder and file workflow and setup, check
out the [prodigenr](https://rostools.github.io/prodigenr) online
documentation.
