# Evaluating the Intensity of the Urban Heat Island in San Salvador, El Salvador
*04.28.2026*

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
This function calculates zonal statistics from multiple rasters (LST) using the LCZ classification by code (shapefile) and save the results to csv format. It uses the following libraries available in Python: os, geopandas, rioxarray, geocube, and xrspatial. In the function it asks to provide the input data in raster format(tif) LST.  The section that generates the zonal statistics is required to provide the shapefile that will be used for the zonal statistics, the name of the output folder, and the column of the shapefile that will be used for the statistical analysis. 

* The result is multiple tables in csv format in a folder. Each csv file contains the results of the individual results of each of the rasters (LST) by the shapefile (LCZ code). 

**2. Concatenate all individual  tables into one single table:**
The function concatenates all the single tables (csv)  into one single table (csv).

**3. Performs t-test to assess statistical significance:**
This function performs independent t-test on two columns from the same CSV. This function compares the statistical significance of the mean, max, and minimum LST  results of  code 801 and 1001 (high percentage of impervious surface and minimum urban vegetation) with code 802 and 1002 (build areas with less percentage of impervious surfaces with higher urban vegetation). 

* The results of this analysis indicated that there is a statistical significance (mean: p-value 0.000, max: p-value 0.0333, minimum: p-value 0.0146) between urban areas (LCZs 1,2,3) and rural areas (LCZ 6 and 9).

**4. Plot of the results:**
This function uses the “boxplot” function of the seaborn library to display the distribution of the data and compare the results. For the time series analysis plot, it uses “lineplot” function which is used to show trends over time visualizing the relationship between two variables. 

* The results show that May has the highest LST and December the lowest LST for all the LCZs (code).

<img width="366" height="278" alt="image" src="https://github.com/user-attachments/assets/e093fade-6da1-4f8a-9b31-c7186190f78c" />

**Figure 1.** Average UHI per LCZ.

## Outcomes
1. This Python-based code can be used to replicate and upscale the analysis to other years and places. 

2. Statistical significance analysis of the comparison of LST between urban areas (LCZ 1,2,3) and rural areas (LCZ 6 and 9) for 2025 for San Salvador, El Salvador. 

3. Plotting of the results using boxplot and ineplot, to visualize the distribution of the data and the timeseries analysis. 

## References
* Jamei, E.,  Ossen, D.R., Seyedmahmoudian, M., Sandanayake, M., Stojcevski, A., Horan, B. 2020. Urban design parameters for heat mitigation in tropics. Renewable and Sustainable Energy Reviews, Volume 134, 2020, 110362, ISSN 1364-0321. https://doi.org/10.1016/j.rser.2020.110362.

* National Oceanic and Atmospheric Administration (NOAA). 2024. Weather Related Fatality and Injury Statistics. Web page. https://www.weather.gov/hazstat. Accessed 04/2026.

* Oke, T.R. 1973. City size and the urban heat island. Atmospheric Environment, 7(8): 769-779. https://doi.org/10.1016/0004-6981(73)90140-6.

* Oke, T.R., Mills, G., Christen, A., Voogt, J.A. 2017. Urban Climates. Cambridge University Press. Cambridge, UK. ISBN: 9780521849500, 0521849500. 525 pp.

* Rahmani, N., Sharifi, A. 2025. Urban heat dynamics in Local Climate Zones (LCZs): A systematic review. Building and Environment, 267 (B), 112225. https://doi.org/10.1016/j.buildenv.2024.112225.

* Son, N.T., Chen, C.F., Chen, C.R. 2020. Urban expansion and its impacts on local temperature in San Salvador, El Salvador. Urban Climate, 32: 100617. https://doi.org/10.1016/j.uclim.2020.100617.

* Stewart, I.D. & T.R. Oke. 2012. Local Climate Zones for Urban Temperature Studies. Bulletin of the American Meteorological Society, 93(12): 1879-1900. https://doi.org/10.1175/BAMS-D-11-00019.1.

* United Nations World Health Organization (WHO). 2025. Heatwaves. Web page. https://www.who.int/health-topics/heatwaves/. Accessed 04/2026.

* Wei, L., Sobrino, J.A. 2024. Surface urban heat island analysis based on local climate zones using ECOSTRESS and Landsat data: A case study of Valencia city (Spain). International Journal of Applied Earth Observation and Geoinformation, 130: 103875. https://doi.org/10.1016/j.jag.2024.103875.





