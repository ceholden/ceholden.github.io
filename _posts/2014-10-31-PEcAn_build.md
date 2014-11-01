---
layout: post
title: PEcAn on SCC/GEO
permalink: PEcAn_on_SCC
tags: [R, SCC, rgdal, BU]
summary: How to compile and install PEcAn with dependencies on GEO/SCC 
comments: true
---

Our university runs a massive computing cluster with software managed using the [Environment Module Project](http://modules.sourceforge.net/) `module` utility. While this software makes managing large collections of programs and libraries, many with long dependency chains and specific version requirements, possible, it means that our `lib` and `include` folders are in non-standard locations. While this isn't a problem, it does make some activities more difficult or impossible for user lacking knowledge of build systems.

To demonstrate I will provide some build details for the `PEcAn` R library:

# PEcAn

The [Predictive Ecosystem Analyzer (PEcAn)](https://github.com/PecanProject/pecan) is an "integrated ecological bioinformatics toolbox". Being such a large project that deals with many data formats, it has a long list of dependencies.

## Download

To get started, I will clone the PEcAn repository:

``` {.bash}
> git clone https://github.com/PecanProject/pecan.git
> cd pecan/
```

Next, I will make sure that R knows where my `R_LIBS_USER` folder is located by setting the environmental variable:

``` {.bash}
> export R_LIBS_USER=/usr3/graduate/ceholden/R_TEST/x86_64-unknown-linux-gnu-library/3.1
```

Note that this is not my usual `R_LIBS_USER` directory, but one I am creating just for this exercise.

``` {.bash}
> mkdir -p $R_LIBS_USER
```

## R

I will be installing `PEcAn` using `R` version 3.1.0 ("Spring Dance").

``` {.bash}
> module load R_earth/3.1.0
```

***Note***: 
> For the sake of demonstration, I will force the PEcAn install script to install a new version of `rgdal` to show how to compile it manually. The `R_earth/3.1.0` module already comes with `rgdal`, but what if we wanted a more recent version?

## Dependencies

PEcAn comes with an Rscript that will take care of most of the dependencies. Note that I have piped the standard error and output to `tee` so that I can view the output in the console while saving it to a text file for further analysis.

``` {.bash}
> R CMD scripts/install.dependencies.R 2>&1 | tee pecan_install.log
```

The script begins by stating what will be installed:

``` {.R}
[1] "installing : "
 [1] "abind"       "car"         "chron"       "coda"        "data.table" 
 [6] "doSNOW"      "dplR"        "earth"       "emulator"    "ggmap"      
[11] "ggplot2"     "gridExtra"   "Hmisc"       "kernlab"     "knitr"      
[16] "lubridate"   "MASS"        "MCMCpack"    "mvtnorm"     "ncdf4"      
[21] "plotrix"     "plyr"        "raster"      "randtoolbox" "rjags"      
[26] "rgdal"       "tgp"         "DBI"         "roxygen2"    "stringr"    
[31] "testthat"    "XML"         "RNCEP"       "foreign"     "RCurl"      
[36] "udunits2"    "RPostgreSQL" "rPython"
```

The installation will take a long time, but most packages built without issue. At the end, R shows a report of the libraries that failed to install. Packages that cannot be installed automatically in our cluster environment need to be given some extra help in the `configure` phase of the compilation (Remember: our `lib` and `include` directories it tries to find are all over the place).

At the very end of running the `install.dependencies.R` script, R spat out the following messages:

```
Warning messages:
1: In install.packages(new.packages, repos = "http://cran.rstudio.com/") :
  installation of package 'rgdal' had non-zero exit status
2: In install.packages(new.packages, repos = "http://cran.rstudio.com/") :
  installation of package 'udunits2' had non-zero exit status
3: In install.packages(new.packages, repos = "http://cran.rstudio.com/") :
  installation of package 'rPython' had non-zero exit status
4: In install.packages(new.packages, repos = "http://cran.rstudio.com/") :
  installation of package 'rjags' had non-zero exit status
5: In install.packages(new.packages, repos = "http://cran.rstudio.com/") :
  installation of package 'RPostgreSQL' had non-zero exit status
```

To finish the installation of these packages, we'll work through them one by one. The installation errors can be diagnosed in the `configure` stage. 

***NOTE***
> The latest versions of these dependencies have likely changed. Please the appropriate links on your favorite CRAN mirror and update the links accordingly.

### rgdal

```{.bash}
> wget http://cran.r-project.org/src/contrib/rgdal_0.9-1.tar.gz
> tar xvf rgdal_0.9-1.tar.gz
> cd rgdal/
> module load gdal/1.10.0
> ./configure
> cd ../
```

The configuration script was able to find our GDAL installation location because `gdal-config` was in the `PATH` after we loaded the `gdal/1.10.0` module. Unfortunately,

``` {.bash}
checking for proj_api.h... yes
checking for pj_init_plus in -lproj... no
configure: error: libproj not found in standard or given locations.
```

We can resolve this by adding a couple `--with-*` flags (see `./configure --help` for the specifics). We can pass these arguments to the configuration stage within an R installation using `--configure-args`:

```
> module load gdal/1.10.0
> R CMD INSTALL --configure-args="--with-proj-include=/project/earth/packages/proj-4.8.0/include --with-proj-lib=/project/earth/packages/proj-4.8.0/lib --with-proj-share=/project/earth/packages/proj-4.8.0/share/proj" rgdal_0.9.1.tar.gz
```

Success!
  
### udunits

Similarly, we need to load the `udunits` compiled library before we'd have any hope of installing the R bindings to it:

```{.bash}
> module load udunits/2.1.24
> wget http://cran.rstudio.com/src/contrib/udunits2_0.6.tar.gz
> R CMD INSTALL --configure-args="--with-udunits2=/project/earth/packages/udunits-2.1.24/" udunits2_0.6.tar.gz
```

Success!

### rPython

This one gave me the most difficulty. Maybe it's me, but I couldn't figure out how to pass the correct location of the Python shared library files during the linking stage of the compilation. Eventually, I checked the configure script, did some searching, and found that `MAKEFLAGS` was the thing that I needed to specify to correctly pass `LDFLAGS`:

```{.bash}
> module load python/2.7.5
> export MAKEFLAGS='LDFLAGS=-L/project/earth/packages/Python-2.7.5/lib'
> wget http://cran.rstudio.com/src/contrib/rPython_0.0-5.tar.gz
> R CMD INSTALL rPython_0.0-5.tar.gz
```

Success!

### rjags

`rjags` requires the JAGS library be installed. Luckily this is already available as module:

```{.bash}
> module load jags/3.4.0
> wget http://cran.r-project.org/src/contrib/rjags_3-14.tar.gz
> R CMD INSTALL --configure-args="--prefix=/project/earth/packages/JAGS-3.4.0/bin --with-jags-lib=/project/earth/packages/JAGS-3.4.0/lib --with-jags-include=/project/earth/packages/JAGS-3.4.0/include/JAGS" rjags_3-14.tar.gz
```

Success!

### RPostgreSQL

And finally the last R package that needs a pre-built library installed:

``` {.bash}
> module load postgresql/9.2.4
> wget http://cran.r-project.org/src/contrib/RPostgreSQL_0.4.tar.gz
> tar xvf RPostgreSQL_0.4.tar.gz
> R CMD INSTALL RPostgreSQL_0.4.tar.gz
```

Success!

## PEcAn Installation

With all the dependencies installed, we can finally install PEcAn:

Load required modules:

```{.bash}
> module load udunits2/2.1.24
> module load R_earth/3.1.0
> module load gdal/1.10.0
> module load postgresql/9.2.4
> module load jags/3.4.0
```

Clone PEcAn repository and build:

``` {.bash}
> git clone https://github.com/PecanProject/pecan.git
> cd pecan/
> ./scripts/build.sh
```

The build script will take some time building all of the submodules, but it will show the success/failure of each submodule as it goes.

## PEcAn module

Now that PEcAn is built for my own `R_LIBS_USER` directory, we can copy it somewhere to make it globally available by creating a module for the libraries. This module will be seen by R if we add the location to the `R_LIBS_SITE` environment variable. 

The idea is that this location will serve as a repository for a basic set of installation dependencies for PEcAn. If a user wants to upgrade PEcAn, they can re-build it and install it into their local `R_LIBS_USER` folder which will take precedence. Similarly, any dependencies that are upgraded by the user will take precedence over the libraries installed in this module. For confirmation of this behavior, see the [documentation R provides about packages for the Debian Linux distribution](http://cran.r-project.org/bin/linux/debian/README.html).

Another way of testing this behavior is using the `.libPaths()` command within R as [described here](https://stat.ethz.ch/R-manual/R-devel/library/base/html/libPaths.html). For example:

``` {.R}
> .libPaths()
[1] "/usr3/graduate/ceholden/R/x86_64-unknown-linux-gnu-library/3.1"
[2] "/project/earth/packages/R-3.1.0/lib64/R/library"
```

With the package dependencies copied over to a globally accessible and backed up location, we can write the module file as follows:

``` {.bash}
#%Module 1.0
#

proc ModulesHelp { } {
    puts stdout "PEcAn - Predictive Ecosystem Analyzer"
    puts stdout ""
    puts stdout "Cloned on 10/23/2014"
    puts stdout "47321aa1fb612fe6327b2f557785f5da8360c6dc"
    puts stdout ""
    puts stdout "http://pecanproject.github.io/"
    puts stdout ""
}
module-whatis "Sets the environment for PEcAn in R"

set topdir /project/earth/packages/PEcAn/

module load R_earth/3.1.0
module load udunits/2.1.24
module load postgresql/9.2.4
module load jags/3.4.0

prepend-path R_LIBS_SITE $topdir/R_LIBS/
```

To use this module, simply load it as normal:

``` {.bash}
module load PEcAn/latest
```

As a test of whether or not the load order is correctly specified, you can check the library order within R:

``` {.R}
> .libPaths()
[1] "/usr3/graduate/ceholden/R/x86_64-unknown-linux-gnu-library/3.1"
[2] "/project/earth/packages/PEcAn/R_LIBS"                          
[3] "/project/earth/packages/R-3.1.0/lib64/R/library"
```

