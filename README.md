## Summary
This repository documents the data processing and the analysis performed on the data to support the findings presented in the article **"Socio-Spatial Inequality and the Effects of Density on COVID-19 Transmission in U.S. Cities"** published in *Nature Cities*.

## Title: Socio-Spatial Inequality and the Effects of Density on COVID-19 Transmission in U.S. Cities

**Authors**: [Constantine E. Kontokosta](https://marroninstitute.nyu.edu/people/constantine-kontokosta)<sup>1,2,3,*</sup>, [Boyeong Hong](https://marroninstitute.nyu.edu/people/boyeong-hong)<sup>1</sup>, and [Bartosz J. Bonczak](https://marroninstitute.nyu.edu/people/bartosz-bonczak)<sup>1,2,3</sup>

<sup>1</sup>[New York University, Marron Institute of Urban Management, 370 Jay St 12th floor, Brooklyn, NY 11201](https://marroninstitute.nyu.edu/)

<sup>2</sup>[New York University, Tandon School of Engineering, 6 MetroTech Center, Brooklyn, NY 11201](https://engineering.nyu.edu)

<sup>3</sup>[New York University, Center for Urban Science and Progress, 370 Jay Street, Brooklyn, NY 11201](https://cusp.nyu.edu/)

<sup>*</sup>Correspondence and requests for materials should be addressed to Constantine E. Kontokosta (email: <ckontokosta@nyu.edu>).

![Figure 1](https://github.com/UrbanIntelligenceLab/neighborhood-density-mitigating-behavior-and-the-inequality-of-covid-19-transmission-in-us-cities/blob/main/figure1.png?raw=true)

## Abstract
Cities are often associated with the rapid spread of infectious diseases, driven by the perceived risks of urban density and overcrowding. However, transmission risk can vary considerably within urbanized areas as a function of socio-spatial disparities and the adoption of mitigating behaviors across communities. In this study, we examine the effect of density on COVID-19 infection rates at the neighborhood scale within and across U.S. cities. We integrate high spatial resolution measures of land use and residential population density, mobility, infection rates, and social determinants of health to evaluate the impact of neighborhood context on infection risk, while controlling for the potential mitigating effects of social distancing behavior. We are particularly focused on disparities among marginalized and vulnerable neighborhoods and the generalizability of the results across political, socioeconomic, regional, and built environment contexts in the U.S. Our findings demonstrate a non-linear relationship between urban density and infection rates, with higher density neighborhoods more likely to adopt mitigating behaviors to reduce transmission. However, low-income and minority communities, facing cascading health challenges, are found to be least able to modify mobility behavior and therefore experienced a disproportionate burden of COVID-19 infection risk during the first wave of the pandemic.

## Cite
Kontokosta, C. E., Hong, B., & Bonczak, B. (in press). Socio-Spatial Inequality and the Effects of Density on COVID-19 Transmission in U.S. Cities. *Nature Cities*

## Repository Structure
The repository documents the data processing and analysis perform on the data to support the findings of the study reported in the published article. It is structured as follows:

```
.\root
    |--- data                   # placeholder directory intended to contain raw data
    |--- figures                # figures generated for the publication purposes
    |--- scripts                # contains all scripts used in the study 
         |--- data_processing   # scripts processing raw data with PySpark on HDFS cluster
         |--- analysis          # scripts documenting analytical tasks
```

## Data Description

### Mobility Data
The primary data used for the main analysis are the annonymized geolocated mobile application activity provided by [VenPath, Inc.](https://www.venpath.net/) – a data marketplace company providing mobile application data and business analytics services extracted from more than 200 various mobile applications and covering more than 120 million devices every month across the U.S. The initial dataset of approximately 250 billion geotagged data points associated with 4.5 million unique devices hourly and covers the period from February 1st to July 13th of 2020.

### Land Use Data
For the purpose of assigning an activity type to the mobility geolocation data, we used a range of city-specific land use data combined with building footprint data, administrative boundaries, and road network data. These data were sourced from official administrative records obtained through publicly-available open data platforms. Local road network data was obtained for each city from the OpenStreetMap platform using QGIS software with dedicated plugins. Each data layer was converted into the Geographic Coordinate System corresponding with the mobility data and clipped to the local municipality (city) boundary extent. A full list of ancillary data used for this rasterization process and analysis is provided in the Supplementary Information, Table S7.

### COVID-19 Case Rate Data
In order to examine neighborhood-level COVID-19 infection rates, we collect available data on confirmed COVID-19 cases for twelve (12) cities from multiple data sources at the zip code level (localized COVID-19 data were not available for three of the initial sample of fifteen cities). Based on the number of reported COVID-19 cases for each city, we use spatial interpolation to adjust to the census tract level. Specifically, the infection rate is defined as the number of confirmed cases per 100,000 residential population. COVID-19 case data sources are presented in the Supplementary Information (Table S8). 

### Ancilliary Data
We retrieve multiple ancillary datasets for neighborhood demographic, socioeconomic, and political characteristics. We use the [2019 5-year estimate U.S. Census Bureau's American Community Survey (ACS)](https://www.census.gov/programs-surveys/acs/technical-documentation/table-and-geography-changes/2019/5-year.html) database for census tract data on race, ethnicity, household type, housing, income, and job occupation attributes. Voting patterns and political affiliation are extracted from the standardized precinct 2020 presidential data, developed and shared by the [New York Times](https://github.com/TheUpshot/presidential-precinct-map-2020). We also obtain census tract data on neighborhood health conditions, specifically chronic disease and health indicators provided by the [Centers for Disease Control and Prevention](https://chronicdata.cdc.gov/500-Cities-Places/PLACES-Local-Data-for-Better-Health-Census-Tract-D/cwsq-ngmh). We use these data to estimate the percentage of neighborhood residents with underlying medical conditions. These datasets are publicly-available and acquired from open data platforms and government databases. 

## System Specifications
Mobility data were provided via dedicated AWS S3 service and were managed in accordance with NYU Institutional Review Board approval IRB-FY2018-1645 and stored and accessed in a secured environment at [New York University’s Center for Urban Science and Progress](cusp.nyu.edu) (NYU CUSP) [Research Computing Facility](https://datahub.cusp.nyu.edu/) (RCF), which is equipped with High Performance Computing (HPC) infrastructure, controlled access, and restricted connectivity. Raw data was deployed to Hadoop Cloudera cluster of 20 nodes with 256 GB memory and 2.1 GHz CPU speed each with a total of 1280 cores and 5.1 TB memory. Initial data processing was conducted using [Apache PySpark](https://spark.apache.org/docs/latest/api/python/index.html) version 2.4. The following analysis performed on the processed data was conducted on RCF's High Memory computing server with total memory of 1TB and Intel(R) Xeon(R) CPU E5-4640 0 @ 2.40GHz (4x8 cores) using predominantly [Python](https://www.python.org/) version 3.8 and [Quantum GIS](https://www.qgis.org/en/site/index.html) version 3.4 Madeira. Each script file relies on a separate set of libraries, which were listed at the begining of each of the file, including library version used for the particular task.

## Data Availability Statement
The data used to conduct the analyses described here are summarized in Table S6, Table S7, and Table S8. Processed, aggregate data derived from publicly-available, open data sources that support the findings of this study are available via the dedicated data repositories. The rasterized land use classification data for selected US cities is available in New York University's UltraViolet repository with the identifier of [https://doi.org/10.58153/t7m6v-37090](https://doi.org/10.58153/t7m6v-37090). The dataset of zipcode-level COVID-19 case rates that was used in this study is also available in the NYU's UltraViolet platform with the identifier of [https://doi.org/10.58153/avp10-a8h86](https://doi.org/10.58153/avp10-a8h86). The primary mobility data that support the findings of this study are available from VenPath, Inc., but restrictions apply based on a data sharing agreement. The aggregated neighborhood level exposure density metrics along with the corresponding code are available in the dedicated GitHub repository.

## Acknowledgements
This work was supported, in part, by National Science Foundation awards no. 2028687 and no. 2040898. The study was approved by NYU Institutional Review Board IRB-FY2018-1645, as updated. We would like to thank Professor Lorna Thorpe and Professor Arpit Gupta for their feedback on preliminary versions of this methodology, and to Arpit Gupta for access to VenPath, Inc. data. All errors remain our own.

## License

MIT License

Copyright (c) 2023 Urban Intelligence Lab

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
