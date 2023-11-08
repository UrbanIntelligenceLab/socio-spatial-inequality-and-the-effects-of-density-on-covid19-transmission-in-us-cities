# Summary
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

# Repository Structure
The repository documents the data processing and analysis perform on the data to support the findings of the study reported in the published article. It is structured as follows:

```
.\root
    |--- data                   # placeholder directory intended to contain raw data
    |--- figures                # figures generated for the publication purposes
    |--- scripts                # contains all scripts used in the study 
         |--- data_processing   # scripts processing raw data with PySpark on HDFS cluster
         |--- analysis          # scripts documenting analytical tasks
```

# Data Description

## Mobility Data
The primary data used for the main analysis are the **annonymized geolocated mobile application activity** provided by [VenPath, Inc.](https://www.venpath.net/) – a data marketplace company providing mobile application data and business analytics services extracted from more than 200 various mobile applications and covering more than 120 million devices every month across the U.S. The initial dataset of approximately 250 billion geotagged data points associated with 4.5 million unique devices hourly and covers the period from February 1st to July 13th of 2020.

### Data Availability Statement
The annonymized geolocated mobile application activity data that support the findings of this study are available from VenPath, Inc. but restrictions apply to the availability of these data, which were used under license for the current study, and so are not publicly available. Data are however available from the authors upon reasonable request and with permission of VenPath, Inc.

# System Specifications
Mobility data were provided via dedicated AWS S3 service and were managed in accordance with NYU Institutional Review Board approval IRB-FY2018-1645 and stored and accessed in a secured environment at [New York University’s Center for Urban Science and Progress](cusp.nyu.edu) (NYU CUSP) [Research Computing Facility](https://datahub.cusp.nyu.edu/) (RCF), which is equipped with High Performance Computing (HPC) infrastructure, controlled access, and restricted connectivity. Raw data was deployed to Hadoop Cloudera cluster of 20 nodes with 256 GB memory and 2.1 GHz CPU speed each with a total of 1280 cores and 5.1 TB memory. Initial data processing was conducted using [Apache PySpark](https://spark.apache.org/docs/latest/api/python/index.html) version 2.4. The following analysis performed on the processed data was conducted on RCF's High Memory computing server with total memory of 1TB and Intel(R) Xeon(R) CPU E5-4640 0 @ 2.40GHz (4x8 cores) using predominantly [Python](https://www.python.org/) version 3.7 and [Quantum GIS](https://www.qgis.org/en/site/index.html) version 3.4 Madeira. Each script file relies on a separate set of libraries, which were listed at the begining of each of the file, including library version used for the particular task.

# License

MIT License

Copyright (c) 2021 Urban Intelligence Lab

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
