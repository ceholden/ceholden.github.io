% Landsat timeseries classification for monitoring land cover change and transitions
% Chris Holden
% December 12, 2014

# Why?

## 

<img src="media/IPCC_AR5_net_LCLUC.png" height="800">
<br>

IPCC 5th Assessment Report

## Why?

* Proxy for biogeochemical processes and energy balance
* Competition among land uses
* Subject to continue changing

# Land Cover

## How: traditionally?

* Passive optical measurement of radiation
* Stable classes inferred from spectral and spatial context
* Change assessed using several "snapshots" in time
    - Change between stable classes
    - Epochs (*e.g.*, ~1990 - 2000, 2000 - 2010)

# Land Cover

## How: recently?

<img src="media/2014_kennedy_remote_sensing_era.png" height=500 width=600)
<br>

Kennedy *et al.* 2014 

"Bring an ecological view of change to Landsat-based remote sensing"

## Why not use all the data?
<br>
<br>

* **Some of the data**
    * Vegetation Change Tracker (VCT) (Huang *et al* 2010)
    * LandTrendr (Kennedy *et al* 2010)
    * Hansen *et al* 2013
* **Most of the data**
    * Break detection For Additive and Seasonal Trends (BFAST) (Verbesselt *et al* 2012)
    * Continuous Change Detection and Classification (CCDC) (Zhu and Woodcock 2014)

## These algorithms have (mostly) only been applied to forests conversion
<br>

# Example

##

<img src="media/mass/1_pontus_2obs.jpg" height=500>

NIR reflectance - 2 observations

##

<img src="media/mass/3_pontus_yearly.jpg" height=500>

NIR reflectance - growing season observations

## 

<img src="media/mass/4_pontus_summer_winter.jpg" height=500>

NIR reflectance - growing and leaf-off observations

##

<img src="media/mass/5_pontus_alldata.jpg" height=500>

NIR reflectance - all available\* observations

##

<img src="media/mass/6_pontus_all_model.jpg" height=500>
<br>

NIR reflectance - CCDC model fit

## 

<img src="media/mass/7_pontus_vhr.png" height=700>

# Research Questions

##

<div style="font-size: 1.25em">
1. What "spectro-temporal" signatures are most important for separating land cover classes?<br><br>
2. Can transitional subclasses be reliably identified?
3. How do observations conditions influence "spectro-temporal" signatures?
</div>

# Land Cover Trends

##
<img src="media/LCT_ecoregions.jpg" height=700>

**Land Cover Trends Ecoregions**

## Land Cover Trends

<img src="media/LCT_classes.jpg" height="400" width="800">

**Epochs:** 1972, 1980, 1986, 1992, 2000

---

### Stand Age / Regrowth Trajectory

* <span style="color:red">Non-Forest</span> in 1992 to <span style="color:green">Forest</span> in 2000
* <span style="color:red">Non-Forest</span> in 1986 to <span style="color:green">Forest</span> in 2000
* <span style="color:red">Non-Forest</span> in 1980 to <span style="color:green">Forest</span> in 2000
* <span style="color:red">Non-Forest</span> in 1972 to <span style="color:green">Forest</span> in 2000

# "Spectro-Temporal" signatures

##

<img src="media/speclab_usgs_veg.gif" height="750">

<http://speclab.cr.usgs.gov/>

## Note:

The following plots show mean coefficient values with standard deviation error bars for timeseries models matching Land Cover Trends classes for the year 2000. Number of pixels in each average varies by class, but herb/shrub, agriculture, and forest usually have 5,000+ pixels across several sample blocks

Plot labels:

- "beta0" - intercept
- "beta1" - slope
- "amp1" - 1 year period sine/cosine amplitude
- "amp2" - 1/2 year period sine/cosine amplitude
- "B*" - Landsat TM/ETM band designations

# Colorado

## Forests

##

<img src="media/plots/p034r032_F_NF_intercept.png" width="1250">

##

<img src="media/plots/p034r032_F_NF_slope.png" width="1250">

##

<img src="media/plots/p034r032_F_NF_amplitude1.png" width="1250">

##

<img src="media/plots/p034r032_F_NF_amplitude2.png" width="1250">

##

<img src="media/plots/p034r032_F_NF_RMSE.png" width="1250">

## Agriculture and Grass/Shrubs

##

<img src="media/plots/p034r032_ag_herb_intercept.png" width="1250">

## 

<img src="media/plots/p034r032_ag_herb_slope.png" width="1250">

## 

<img src="media/plots/p034r032_ag_herb_amplitude1.png" width="1250">

##

<img src="media/plots/p034r032_ag_herb_amplitude2.png" width="1250">

## 

<img src="media/plots/p034r032_ag_herb_rmse.png" width="1250">


# Central Valley, California

## 

<img src="media/p043r034/P043R034_GoogleMaps.png" height="800">

##

<img src="media/p043r034/LC_2000.png" height="800">

##

<img src="media/p043r034/LC_2010.png" height="800">

## Forests

##

<img src="media/plots/p043r034_F_NF_intercept.png" width="1250">

##

<img src="media/plots/p043r034_F_NF_slope.png" width="1250">

##

<img src="media/plots/p043r034_F_NF_amp1.png" width="1250">

##

<img src="media/plots/p043r034_F_NF_amp2.png" width="1250">

##

<img src="media/plots/p043r034_F_NF_rmse.png" width="1250">

## Agriculture, Grass/Shrubs, and Developed

##

<img src="media/plots/p043r034_ag_herb_intercept.png" width="1250">

##

<img src="media/plots/p043r034_ag_herb_slope.png" width="1250">

##

<img src="media/plots/p043r034_ag_herb_amp1.png" width="1250">

##

<img src="media/plots/p043r034_ag_herb_amp2.png" width="1250">

##

<img src="media/plots/p043r034_ag_herb_rmse.png" width="1250">

# Florida

## Forests

##

<img src="media/plots/p016r041_F_NF_intercept.png" width="1250">

##

<img src="media/plots/p016r041_F_NF_slope.png" width="1250">

##

<img src="media/plots/p016r041_F_NF_amp1.png" width="1250">

##

<img src="media/plots/p016r041_F_NF_amp2.png" width="1250">

##

<img src="media/plots/p016r041_F_NF_rmse.png" width="1250">

## Agriculture, Grass/Shrubs, and Developed

##

<img src="media/plots/p016r041_ag_herb_intercept.png" width="1250">

##

<img src="media/plots/p016r041_ag_herb_slope.png" width="1250">

##

<img src="media/plots/p016r041_ag_herb_amp1.png" width="1250">

##

<img src="media/plots/p016r041_ag_herb_amp2.png" width="1250">

##

<img src="media/plots/p016r041_ag_herb_rmse.png" width="1250">


# Conclusions

##

1. Linear regression intercepts behave similarly to single date spectral reflectances
2. Seasonal dynamics and large temporal variability (high RMSE) help distinguish agriculture from unmanaged fields
3. Regrowth signal of forest disturbance can persist after decades
4. Regrowth signal visibility strongly affected by climate (CA & CO, versus FL)

# BRDF

## Note:

- Path/Rows: p034r032 (sunlit) and p035r032 (shaded)
- Land Cover Trends sample: samp21_0122, samp21_0235, samp21_0341
    + Note: samp21_0235 had vast majority of forest regrowth pixels
- Plots generated by land cover class and spectral band
- Intercepts behave as normal spectral signals
- Slopes were surprising for me and I'm not really sure what the mechanism is behind the patterns

## Intercepts

##

<img src="media/BRDF/path_row_intercept_one_to_one_0.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_1.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_2.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_3.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_4.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_5.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_6.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_7.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_8.png" width="1250">

##

<img src="media/BRDF/path_row_intercept_one_to_one_9.png" width="1250">

## Slopes

##

<img src="media/BRDF/path_row_slope_one_to_one_0.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_1.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_2.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_3.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_4.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_5.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_6.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_7.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_8.png" width="1250">

##

<img src="media/BRDF/path_row_slope_one_to_one_9.png" width="1250">

## Conclusions

- BRDF affects intercepts as expected
- Non-zero slopes in forests are biased
    + Visible/SWIR slopes larger for sun-lit (p034r032)
    + NIR slopes larger for sun-shaded (p035r032)
- Older forests have less bias in intercept 
    + See stable forest versus NF86->F (was not forest in 86, was in 92 and 2000)
- Directionality important factor in spectro-temporal signatures
- Some previous work of mine suggests combined timeseries introduce additional noise, but result in non-biased models (next thing for me to test!)
