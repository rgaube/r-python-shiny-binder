[![Binder](http://mybinder.org/badge_logo.svg)](http://mybinder.org/v2/gh/rgaube/r-python-shiny-binder/master?urlpath=rstudio) Launch RStudio

[![Binder](http://mybinder.org/badge_logo.svg)](http://mybinder.org/v2/gh/rgaube/r-python-shiny-binder/master?urlpath=shiny/bus-dashboard/) Launch RShiny

[![Binder](http://mybinder.org/badge_logo.svg)](http://mybinder.org/v2/gh/rgaube/r-python-shiny-binder/master?urlpath=lab) Launch Jupyter Lab

# R + Python + Shiny Binder Example

This repository is a combination of these two templates provided by binder-examples repositories:
- https://github.com/binder-examples/r
- https://github.com/binder-examples/r_with_python

Potentially interesting is also the following template:
- https://github.com/binder-examples/apt_install

This repo builds on the [r binder](https://github.com/binder-examples/r) and [jupyter lab binder](https://github.com/binder-examples/jupyterlab) and is complementary to the [multi-language-demo binder](https://github.com/binder-examples/multi-language-demo) with examples on using both R and python in both Jupyter Lab and RStudio.

Example files included:

 - `python_example_for_Jupyter.ipynb` - Notebook file using a python kernel for working in Jupyter
 - `R_example_for_Jupyter.ipynb` - Notebook file using an R kernel for working in Jupyter
 - `python_example_for_RStudio.Rmd` - RMarkdown file with python code chunks for working in RStudio
 - `R_example_for_RStudio.Rmd` - RMarkdown file with R code chunkcs for working in RStudio

Note: to mix R and python in a single Jupyter notebook, use cell magic as demonstrated in the [multi-language-demo](https://github.com/binder-examples/multi-language-demo) binder examples. To mix R and python in a single RMarkdown file (and exchange information between them), make use of [reticulate](https://rstudio.github.io/reticulate/). The latter requires [RStudio 1.2+](https://www.rstudio.com/products/rstudio/download/preview/) to work interactively, which is not yet installed as the default binder version (i.e. interactive python and python plots will not yet work in RMarkdown and the above example file uses reticulate for plotting in the knitted file).

## Binder Setup

Modify the files in the `binder` sub-directory to specify required dependencies for R and python. Binder will generate a docker image for your repository after every change to the repo and then will re-use the docker image on subsequent launches. This means that the first time you launch binder for the latest version of your branch, it may take some time to launch (especially with a lot of R dependencies which are all compiled from source) but will be fast for everyone else afterwards. Switching between `RStudio` vs. `Jupyter Lab` as the IDE is accomplished easily by changing the binder link as described below - the required dependencies for both are automatically installed and do not need to be explicitly listed in the respective configuration files.

**Important**: binder will *only* work for public repositories. If your repository is private, you will have to make it public in the repository settings before you can launch it in binder.

## R

## binder/runtime.txt

Binder supports using R and RStudio, with libraries pinned to a specific 
snapshot on [MRAN](https://mran.microsoft.com/documents/rro/reproducibility).

You need to have a `runtime.txt` file that is formatted like `r-<YYYY>-<MM>-<DD>` where YYYY-MM-DD is a snapshot at MRAN that will be used for installing libraries. 
In this line, you can request a [specific version of R](https://github.com/jupyter/repo2docker/pull/772#issue-313426641). 
To do this list the version between the 'r' and the year, as in `r-3.6-2019-09-24`. 
Right now the default version of R is 3.6.

## binder/install.R

You can also have an `install.R` file that will be executed during build, and can be used to install libraries. 
Dependencies can be from CRAN, bioconductor or GitHub. Since GitHub hosted libraries are not part of the MRAN snapshot, it is best to specify a commit or release tag to ensure that a compatible version of the package is installed in the binder.

Both [RStudio](https://www.rstudio.com/) and [IRKernel](https://irkernel.github.io/) are installed by default, so you can use either the Jupyter notebook interface or the RStudio interface.

## Shiny

This repository also contains an example of a Shiny app.

Last, note that if your Binder URL points to a folder, as in http://mybinder.org/v2/gh/binder-examples/r/master?urlpath=shiny/bus-dashboard/, you will need (1) to put in the final slash in the URL, and (2) to avoid converted spaces-'%20'-in the URL, instead placing a hyphen.

## Python

You also need a Python notebook file such as [this one](https://github.com/binder-examples/r/blob/master/index.ipynb).

 - modify the `binder/environment.yml` file to specify the dependencies. The file is a standard [conda environment config file](https://conda.io/docs/user-guide/tasks/manage-environments.html#create-env-file-manually) and thus supports conda packages, version definitions, multiple source channels as well as pip installations.
 - modify the `binder/postBuild` file for any JupyterLab extensions or other direct install commands
