# Evaluating the Intensity of the Urban Heat Island in San Salvador, El Salvador
**Betzy Hernandez Sandoval**, Research Scientist, Earth System Science Center, the University of Alabama in Huntsville (email: betzy.hernandez [at] uah.edu)

*April 29, 2026*

## Description
Developed for [AES508](https://github.com/freemansw1/uah_aes408_508_sp26_public) spring 2026 semester at [the University of Alabama in Huntsville](https://www.uah.edu), this is a Python toolkit that helps decision makers from San Salvador, El Salvador to assess the areas most affected by the **Urban Heat Island (UHI)** effect. The toolkit includes visualization of the areas most affected by heat, statistical analysis, and time series analysis from 2025 using **Land Surface Temperature (LST)** and **Local Climatic Zones (LCZs)**.

## Background
Extreme heat is the leading cause of weather-related deaths globally, causing more fatalities on average than hurricanes, floods, or tornadoes ([NOAA, 2024](https://www.weather.gov/hazstat)). The Urban Heat Island (UHI)  - *a phenomena where urban areas trap heat* - effect amplifies such risk, resulting in hundreds of deaths annually ([Jamei et al. 2010](https://doi.org/10.1016/j.rser.2020.110362), [WHO, 2024](https://www.who.int/health-topics/heatwaves/)). Earth observation data, primarily from NASA satellites and sensors like [Landsat](https://science.nasa.gov/mission/landsat/) and [ECOSTRESS](https://ecostress.jpl.nasa.gov/), has been widely used to map UHI and LCZs by analyzing LST, building morphology, and vegetation cover ([Wei & Sobrino, 2025](https://doi.org/10.1016/j.jag.2024.103875)). These methodologies identify high-intensity heat areas and classify landscapes into standardized zones to study thermal characteristics. LCZs represent a standardized framework of 17 classification types (10 urban and 7 natural) used to analyze UHI disparities by relating surface cover and structural geometry to thermal behavior ([Rahmani & Sharifi, 2025](https://doi.org/10.1016/j.buildenv.2024.112225)).

## Objectives
This research focus on analyzing the spatial patterns of LST across the different LCZs in the city of San Salvador, El Salvador, comparing and analyzing the differences in LST between the most compact, impervious, and high-rise urban areas (LCZs 1-3, 8-10), with more vegetated and sparse rural areas (LCZs 6, 9). This study’s main objectives include:
  * identifying the locations of areas most exposed to UHI effect during 2025, and
  * evaluating LST differences between compact, impervious, and high rise urban areas, and more vegetated and sparse rural areas.

This research aims to provide municipal decision-makers with data that can be used to develop strategies to mitigate UHI effects.


## Methods
The study area is the San Salvador metropolitan area in El Salvador. The city's mean temperature has increased by approximately 1.3°C during the past six decades with projections to continue to increase, and increased urbanization is likely to exacerbate the UHI effect, resulting in public health issues ([Son et al. 2020](https://doi.org/10.1016/j.uclim.2020.100617)).

To estimate **UHI intensity (UHII)**, I used [Oke (1973)](https://doi.org/10.1016/0004-6981(73)90140-6)’s methodology, which evaluates the differences between the average and maximum temperatures of urban areas, contrasted with those parameters for nearby rural areas. As an input to this, I derived LCZs for San Salvador, using a range of inputs (mainly from high spatial resolution multispectral imagery), and based on Oke et al. (2017). I reclassified LCZs 1,2,3, as urban areas, and LCZs 6 and 9 as rural. To estimate the mean and maximum temperatures, I used LST data derived from the thermal infrared bands of the [Landsat-8](https://www.usgs.gov/landsat-missions/landsat-8) and [Landsat-9](https://www.usgs.gov/landsat-missions/landsat-9) satellites. 

**Table 1.** Data sources used.

| Code | LCZ | Mean elevation above sea level (m) |
| --- | --- | --- |
| 801 | Group 1: LCZs 1,2,3 | 600 - 800 | 
| 802 | Group 2: LCZs 6,9 | 600 - 800 |
| 1001 | Group 1: LCZs 1,2,3| 800 - 1,000 |
|1002| Group 2: LCZs 6,9 | 800 - 1,000 |

Group 1 includes LCZ 1 (compact highrise), LCZ 2 (compact midrise), and LCZ 3 (compact lowrise). Group 2 includes LCZ 6 (open lowrise) and LCZ 9 (sparsely built).

To estimate the statistical significance of the differences between urban and rural land surface temperatures, I compared the average and maximum temperatures using a t-test to determine if the difference between the urban and rural areas were statistically significant or due to chance, by calculating the p-value. This analysis provides policy-makers with a degree of confidence in the robustness of the analysis and understanding the impacts of vegetation removal on exacerbating the UHI, and identify areas that need to be prioritized for mitigation interventions.

**Data processing in Python:**

**1. Zonal statistics:**
This function calculates zonal statistics from multiple LST rasters, using the LCZ re-classification (in shapefile format) and save the results to CSV format. It uses the following libraries available in Python: [*os*](https://docs.python.org/3/library/os.html), [*geopandas*](https://geopandas.org/en/stable/), [*rioxarray*](https://corteva.github.io/rioxarray/html/rioxarray.html), [*geocube*](https://pypi.org/project/geocube/), and [*xarray-spatial*](https://xarray-spatial.readthedocs.io/en/stable/). In the function it asks to provide the input LST data in raster format (GeoTIFF). The section that generates the zonal statistics is required to provide the shapefile that will be used for the zonal statistics, the name of the output folder, and the column of the shapefile that will be used for the statistical analysis. 

* The result is multiple tables in CSV format in a folder. Each CSV file contains the results of the individual results of each of the rasters (LST) by the shapefile (LCZ code). 

**2. Concatenate all individual  tables into one single table:**
The function concatenates all the multiple individual tables (in CSV format)  into one single table (also in CSV format).

**3. Performs t-test to assess statistical significance:**
This function performs independent t-test on two columns from the same CSV. This function compares the statistical significance of the mean, max, and minimum LST results of code 801 and 1001 (high percentage of impervious surface and minimum urban vegetation) with code 802 and 1002 (build areas with less percentage of impervious surfaces with higher urban vegetation). 

* The results of this analysis indicated that there is a statistical significance (mean: p-value 0.000, max: p-value 0.0333, minimum: p-value 0.0146) between urban areas (LCZs 1, 2, 3) and rural areas (LCZs 6, 9).

**4. Plot of the results:**
This function uses the “boxplot” function of the [*seaborn*](https://seaborn.pydata.org/) library to display the distribution of the data and compare the results. For the time series analysis plot, it uses “lineplot” function to show trends over time visualizing the relationship between two variables. 

* The results show that May has the highest LST and December the lowest LST for all the LCZs.

<img width="366" height="278" alt="image" src="https://github.com/user-attachments/assets/e093fade-6da1-4f8a-9b31-c7186190f78c" />

**Figure 1.** Average UHI per LCZ.

## Outcomes
1. This Python-based code can be used to replicate and upscale the analysis to other years and places. 

2. Statistical significance analysis of the comparison of LST between urban areas (LCZs 1, 2, 3) and rural areas (LCZs 6, 9) for 2025 for San Salvador, El Salvador. 

3. Plotting of the results using boxplot and ineplot, to visualize the distribution of the data and the time series analysis. 

## References
* Jamei, E.,  Ossen, D.R., Seyedmahmoudian, M., Sandanayake, M., Stojcevski, A., Horan, B. 2020. Urban design parameters for heat mitigation in tropics. *Renewable and Sustainable Energy Reviews*, Volume 134, 2020, 110362, ISSN 1364-0321. https://doi.org/10.1016/j.rser.2020.110362.

* National Oceanic and Atmospheric Administration (NOAA). 2024. Weather Related Fatality and Injury Statistics. Web page. https://www.weather.gov/hazstat. Accessed 04/2026.

* Oke, T.R. 1973. City size and the urban heat island. Atmospheric Environment, 7(8): 769-779. https://doi.org/10.1016/0004-6981(73)90140-6.

* Oke, T.R., Mills, G., Christen, A., Voogt, J.A. 2017. Urban Climates. Cambridge University Press. Cambridge, UK. ISBN: 9780521849500, 0521849500. 525 pp.

* Rahmani, N., Sharifi, A. 2025. Urban heat dynamics in Local Climate Zones (LCZs): A systematic review. *Building and Environment*, 267 (B), 112225. https://doi.org/10.1016/j.buildenv.2024.112225.

* Son, N.T., Chen, C.F., Chen, C.R. 2020. Urban expansion and its impacts on local temperature in San Salvador, El Salvador. *Urban Climate*, 32: 100617. https://doi.org/10.1016/j.uclim.2020.100617.

* Stewart, I.D. & T.R. Oke. 2012. Local Climate Zones for Urban Temperature Studies. *Bulletin of the American Meteorological Society*, 93(12): 1879-1900. https://doi.org/10.1175/BAMS-D-11-00019.1.

* United Nations World Health Organization (WHO). 2025. Heatwaves. Web page. https://www.who.int/health-topics/heatwaves/. Accessed 04/2026.

* Wei, L., Sobrino, J.A. 2024. Surface urban heat island analysis based on local climate zones using ECOSTRESS and Landsat data: A case study of Valencia city (Spain). *International Journal of Applied Earth Observation and Geoinformation*, 130: 103875. https://doi.org/10.1016/j.jag.2024.103875.



