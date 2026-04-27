#Trigger model for drought in Afghanistan

developed for FAO Afghanistan by Piotr Wolski in 2025, revised in 2026

Scripts include downloading and preprocessing data as well as the actual generation of the trigger

## Historical data
Historical data are substantial in size (around 1GB) and thus not included in this repo. Data are available from https://web.csag.uct.ac.za/~wolski/fao-afghanistan/


##Downloading
Note: there are four data sources:
1) ENSO - downloaded from psl.noaa.gov
2) ERA5 rainfall - downloaded from CDS
3) ECMWF SEAS51 seasonal forecast of rainfall - downloaded from CDS
4) MODIS MOD11C3 Land Surface Temperature data - downloaded from NASA's EarthData

Downloading of the first three is handled by python script (Step1-3). Downloading of the fourth is dne manually. 

Data downloaded from CDS are a subset covering the region of interest

MODIS data are downloaded as a global dataset, and the subset is extracted at the pre-processing stage.


##Preprocessing
Preprocessing involves:
- derivation of zonal average for each gridded dataset
- calculation of SPI6 from ERA5 rainfall data
- calculation of probability of below normal (lower than 33th percentile) rainfall forecasted by SEAS5.1 system

Output data are a time series of derived variables for each province and are saved into ./data/zonal_data

##Preparation of data file for trigger model

In this step, individual input data (time series of individual variables for each province) are combined into a format suitable for running a regression trigger model. This involves temporal alignment of data. This is necessary because there is a difference between observed and forecasted predictors in the data time - forecast is time stamped to the current month, while observed data are available for the previous month. Drought observations are timestamped to month in the future (target drought period is May)

##Running trigger model
This script implements trigger model and generates figures illustrating its outputs.
