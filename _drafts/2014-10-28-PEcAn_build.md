
---
layout: post
title: PEcAn on SCC/GEO
permalink: PEcAn_on_SCC
tags: [R, SCC, BU]
summary: How to compile and install PEcAn with dependencies on GEO/SCC 
comments: true
---

# PEcAn

PEcAn utility from <https://github.com/PecanProject/pecan>.

Installed dependencies in `scripts/install.dependencies.R`.

Most packages built without issue. The exceptions include:

## Dependencies

### rgdal
1: In install.packages(list.of.packages) :
  installation of package 'rgdal' had non-zero exit status

```{.bash}
module load R_earth/3.1.0
  
wget http://cran.r-project.org/src/contrib/rgdal_0.9-1.tar.gz

R CMD INSTALL --configure-args="--with-proj-include=/project/earth/packages/proj-4.8.0/include --with-proj-lib=/project/earth/packages/proj-4.8.0/lib --with-proj-share=/project/earth/packages/proj-4.8.0/share/proj" rgdal_0.9.1.tar.gz
```
  
### udunits
2: In install.packages(list.of.packages) :
  installation of package 'udunits2' had non-zero exit status

```{.bash}
module load udunits/2.1.24
wget http://cran.rstudio.com/src/contrib/udunits2_0.6.tar.gz

R CMD INSTALL --configure-args="--with-udunits2=/project/earth/packaudunits-2.1.24/" udunits2_0.6.tar.gz
```

3: In install.packages(list.of.packages) :
  installation of package 'rPython' had non-zero exit status

```{.bash}
export MAKEFLAGS='LDFLAGS=-L/project/earth/packages/Python-2.7.5/lib'
wget http://cran.rstudio.com/src/contrib/rPython_0.0-5.tar.gz
R CMD INSTALL rPython_0.0-5.tar.gz
```

4: In install.packages(list.of.packages) :
  installation of package 'rjags' had non-zero exit status

```{.bash}
module load jags/3.4.0
wget http://cran.rstudio.com/src/contrib/rjags_3-13.tar.gz
R CMD INSTALL --configure-args="--prefix=/project/earth/packages/JAGS-3.4.0/bin --with-jags-lib=/project/earth/packages/JAGS-3.4.0/lib --with-jags-include=/project/earth/packages/JAGS-3.4.0/include/JAGS" rjags_3-13.tar.gz
```

## PEcAn Installation

```{.bash}
export R_LIBS_USER=/usr3/graduate/ceholden/R/x86_64-unknown-linux-gnu-library/3.1
```

Load required modules:

```{.bash}
module load udunits2/2.1.24
module load R_earth/3.1.0
module load postgresql/9.2.4
module load jags/3.4.0
```

Clone PEcAn repository and build:

``` {.bash}
git clone https://github.com/PecanProject/pecan.git
cd pecan/
./scripts/build.sh
```

## PEcAn module

Now that PEcAn is built for my own `R_LIBS_USER` directory, we can copy it somewhere to make it globally available by creating a module for the libraries. This module will be seen by R if we add the location to the `R_LIBS_SITE` environment variable. 

The idea is that this location will serve as a repository for a basic set of installation dependencies for PEcAn. If a user wants to upgrade PEcAn, they can re-build it and install it into their local `R_LIBS_USER` folder which will take presidence. Similarly, any dependencies that are upgraded by the user will take preference over the libraries installed in this module. For confirmation of this behavior, see the [documentation R provides about packages for the Debian Linux distribution](http://cran.r-project.org/bin/linux/debian/README.html).

Another way of testing this behavior is using the `.libPaths()` command within R as [described here](https://stat.ethz.ch/R-manual/R-devel/library/base/html/libPaths.html).

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

