# Evaluating the Intensity of the Urban Heat Island in San Salvador, El Salvador
*April 28, 2026*

## Description
This is a Python toolkit that helps decision makers from San Salvador, El Salvador to assess the areas most affected by the Urban Heat Island (UHI) effect. The toolkit includes visualization of the areas most affected by heat, statistical analysis, and time series analysis from 2025 using land surface temperature (LST) and Local Climatic Zones (LCZ).

## Background
Extreme heat is the leading cause of weather-related deaths globally, causing more fatalities on average than hurricanes, floods, or tornadoes (NOAA, 2024). The Urban Heat Island (UHI)  - a phenomena where urban areas trap heat - effect amplifies such risk, resulting in hundreds of deaths annually (Jamei et al. 2010, WHO 2024). Earth observation data, primarily from NASA satellites and sensors like Landsat and ECOSTRESS, has been widely used to map UHI and Local Climate Zones (LCZs) by analyzing Land Surface Temperature (LST), building morphology, and vegetation cover (Wei & Sobrino, 2025). These methodologies identify high-intensity heat areas (UHI) and classify landscapes into standardized zones to study thermal characteristics. LCZs represent a standardized framework of 17 classification types (10 urban and 7 natural) used to analyze UHI disparities by relating surface cover and structural geometry to thermal behavior (Rahmani & Sharifi, 2025).

## Objective
This research focus on analyzing the spatial patterns of LST across the different LCZs in the city of San Salvador, El Salvador, comparing and analyzing the differences between land surface temperature between the most compact, impervious, and high-rise urban areas (LCZs 1-3, 8-10), with more vegetated and sparse rural areas (LCZs 6, 9). This study’s main objectives include: (i) identifying the locations of areas most exposed to  urban heat island (UHI) effect during 2025, and (ii) evaluating LST differences between compact, impervious, and high rise urban areas, and more vegetated and sparse rural areas. This research aims to provide decision-makers with data that can be used to develop strategies to mitigate UHI effects.


## Methods
The study area: San Salvador metropolitan area in El Salvador. The city’s mean temperature has increased by approximately 1.3°C during the past six decades with projections to continue to increase, and increased urbanization is likely to exacerbate the UHI effect, resulting in public health issues (Son et al. 2020).

To estimate UHI intensity (UHII), I used Oke (1973)’s methodology, which evaluates the differences between the average and maximum temperatures of urban areas, contrasted with those parameters for nearby rural areas. As an input to this, I derived LCZs for San Salvador, using a range of inputs (mainly from high spatial resolution multispectral imagery), and based on Oke et al. (2017). I reclassified LCZs 1,2,3, as urban areas, and LCZs 6 and 9 as rural. To estimate the average and maximum temperatures, I used LST data derived from the thermal infrared bands of the Landsat-8 and Landsat-9 satellites. 

**Table 1.** Data sources.

| Code | LCZ | Mean elevation above sea level (m) | 
| --- | --- | --- | 
| 801 | Group 1: LCZ 1,2,3 | 600 - 800 m | 
| 802 | Group 2: LCZ 6,9 | 600 - 800 m |
| 1001 | Group 1: LCZ 1,2,3| 800 - 1000m | 
|1002| Group 2: LCZ 6,9 | 800 - 1000 | 

Group 1 includes LCZ1 (compact highrise), LCZ 2 (compact midrise), and LCZ3 (compact lowrise). Group 2 includes LCZ 6 (open lowrise) and LCZ 9 (sparsely built).

To estimate the statistical significance of the differences between urban and rural land surface temperatures, I compared the average and maximum temperatures using a t-test to determine if the difference between the urban and rural areas were statistically significant or due to chance, by calculating the p-value. This analysis provides policy-makers with a degree of confidence in the robustness of the analysis and understanding the impacts of vegetation removal on exacerbating the UHI, and identify areas that need to be prioritized for mitigation interventions.

**Data processing in Python:**

**1. Zonal statistics:**
This function calculates zonal statistics from multiple rasters (LST) using the LCZ classification by code (shapefile) and save the results to csv format. It uses the following libraries available in Python: os, geopandas, rioxarray, geocube, and xrspatial. In the function it asks to provide the input data in raster format(tif) LST.  The section that generates the zonal statistics is required to provide the shapefile that will be used for the zonal statistics, the name of the output folder, and the column of the shapefile that will be used for the statistical analysis. The result is multiple tables in csv format in a folder. Each csv file contains the results of the individual results of each of the rasters (LST) by the shapefile (LCZ code). 

