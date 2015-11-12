---
title       : Pollution Predictor
subtitle    : Exploring the 2015 EPA air quality dataset
author      : catharpin
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction



Annual average air pollution data is available at the [EPA air quality website](https://www.epa.gov/airdata).
The EPA provides an interactive mapping tool, but it is not available on all platforms due to its
use of the Google Earth browser plugin.  R and the
Shiny platform give us the means to address this shortcoming.

We have demonstrated this using 2015 pollution data for ozone and PM 2.5 particulate matter.

--- .class #id 

## Obtaining the Data Efficiently

We can automate the entire process of obtaining the data and formatting it for use with the application.
Reducing the size of the dataset helps to improve the performance and responsiveness; we also check
to see if we already have the data to avoid downloading it repeatedly.  


```r
if (file.exists("./pollution_data.Rdata")){
  load("./pollution_data.Rdata")
} else {
  if (!file.exists("./annual_all_2015.zip")) {
    download.file("http://aqsdr1.epa.gov/aqsweb/aqstmp/airdata/annual_all_2015.zip", 
                  destfile="annual_all_2015.zip")
  }
# Transformations removed for brevity
  save(pollution_data,file="pollution_data.Rdata")
}
```



--- .class #id 

## Viewing the Results

Our application allows the user to select the pollutant and latitude and longitude of interest to them, displaying it on a US map to assist with
context.  The system will then determine the nearest five monitoring stations reporting data for that pollutant and averages them to produce an estimated average annual pollutant level for that location.  The stations used in this analysis are shown below.

![plot of chunk unnamed-chunk-4](assets/fig/unnamed-chunk-4-1.png) 

--- .class #id 

## Try it Yourself


`https://catharpin.shinyapps.io/bright-shiny-object/`

<img src="app.png" title="Screenshot of the application" height="50%" width="50%">


