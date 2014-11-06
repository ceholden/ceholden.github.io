% Tip of the Week
% Thursday, November 6th, 2014

# Tip: Remote Sensing Utilities

# GDAL

## Command Line Utilities

- Useful for almost all preprocessing
    + Metadata: `gdalinfo`
    + Reproject: `gdalwarp`
    + Format conversion: `gdal_translate`
    + Stack / mosaic: `gdal_merge.py`
    + Vector to Raster: `gdal_rasterize`
- `module load gdal/1.10.0`
- <http://www.gdal.org/gdal_utilities.html>

## API

Write your own code? Use GDAL API:

- Python
    + `module load gdal/1.10.0` (loads `python/2.7.5`)
    + `from osgeo import gdal`
- R (via `rgdal` and `raster` packages)
    + `module load R_earth/3.1.0`
    + `library(raster)`
- C/C++:
    + `module load gdal/1.10.0`
    + `#include "gdal.h"`
    + `GDAL_LIB` and `GDAL_INC` paths

# OGR

## Command Line Utilities

- `ogrinfo`
    + Basic information: `ogrinfo -so -al vector.shp`
    + Simple queries: `ogrinfo -al -where "FEATURE > 5" vector.shp`
    + SQL for more advanced queries (`-sql`)
    + Combine with `grep`, `wc`, etc... to quickly summarize vector data
- `ogr2ogr`
    + Format conversion: `ogr2ogr -f KML vector.kml vector.shp`
    + Reproject: `ogr2ogr -t_srs "EPSG:4326" vector_wgs84.shp vector.shp`
    + Merge: `ogr2ogr -append combined.shp part2.shp`
- <http://www.gdal.org/ogr_utilities.html>

# QGIS

## QGIS v2.0

- On par with ArcGIS in some regards, better than in most.
- Built on GDAL/OGR
- QGIS vs ENVI
- Plugin architecture
- `module load qgis/2.0.1`

# Landsat Data

## Download

[Bulk Download Application](http://earthexplorer.usgs.gov/bulk/) for L1 products:

- `module load bda/1.1.2`
- Use `qsh` session for big downloads -- very CPU intensive!
- Updating is grief inducing... ask IT if update is required

## Preprocess

Parallel SR / Fmask for Landsat 4, 5, 7, and 8 in one command:

- `module load batch_landsat/v4`
- `landsatPrepSubmit.sh -h`
- Surface reflectance only suggested for Landsat 8 (as of Nov 6th, 2014)
    + LEDAPS for Landsat 4/5/7 from ESPA
    + Landsat 8 version still in development
    + We have ancillary data until 2014 DOY 282
- See [tutorial](https://github.com/ceholden/landsat_preprocess) from May 2014

## Visualization

Timeseries interactive visualization in QGIS:

- "Stable" - `module load CCDCTools/latest`
- "Development" - `module load CCDCTools/_beta`

# Version control system (VCS)

## Git

- Usable version on GEO/SCC
- Cannot push / pull using HTTPS
- Must generate crypto keypair and give Github your public key
- <https://help.github.com/categories/ssh/>

# Reproducibility

## IPython Notebook

Use Python? Want to share or explain your work, or just save and document your explorations?

- [Nature - Interactive notebooks: Sharing the code](http://www.nature.com/news/interactive-notebooks-sharing-the-code-1.16261) (doi:10.1038/515151a)
- On GEO:
    + `module load python/2.7.5`
    + `ipython notebook`
    + Remember the port it uses!
- Locally:
    + `ssh -L [local port]:localhost:[remote port] [user]@geo.bu.edu`
    + Visit localhost:[port] in browser
- [Secure your notebook session](http://ipython.org/ipython-doc/1/interactive/public_server.html)

## KnitR

Installed as part of RStudio!
