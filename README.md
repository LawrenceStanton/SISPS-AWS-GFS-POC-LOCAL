# SISPS-AWS-GFS-POC-LOCAL

Proof of Concept for SISPS AWS GFS weather forecasting service.

## Overview

The Global Forecast System (GFS) is a weather forecast model produced by the National Centers for Environmental Prediction (NCEP). The forecast is published every 6 hours to a public AWS S3 bucket. The data is in GRIB2, and various files are uploaded containing a variety of forecast data. The forecast data of interest for this service is primarily temperature. This proof of concept is to demonstrate the ability to download, interpret, and plot temperature data from the GFS forecast for Antarctica and SANAE IV.

## General Considerations

> [!NOTE]  
> More detailed notes are made in [main.ipynb](main.ipynb).

GRIB2 is a binary format, and the data is not easily readable, but can be parsed by a suitable engine into a more generic format such as NetCDF. These data tools are generally available in Python, which determines the choice of language for this service.

The GFS forecast is a global model and each file contains data for the entire planet. Files are separated temporally. Therefore to extract a time series for a specific location, all global files for that time period must be downloaded. This is a significant amount of data, especially at the high resolution scale. A more serialised approach will be needed for systems with limited storage. However, if deployed to AWS within the same region as the GFS bucket, the data transfer costs are zero.
