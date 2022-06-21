# Evictions in New York City

## Table of contents
- [Introduction](#Introduction)
- [Evictions and Income in NYC](#Evictions-and-Income-in-NYC)
- [Using Plotly Express and Mapping with NYC Open Data](#Using-Plotly-Express-and-Mapping-with-NYC-Open-Data)
- [Geocoding with Nominatum and OpenStreetMap](#Geocoding-with-Nominatum-and-OpenStreetMap)

## Introduction
This is an exploratory data analysis of Evictions in NYC. As explained in this [article](https://www.6sqft.com/new-survey-highlights-nycs-rental-housing-crisis-showing-few-affordable-apartments-available/) by Michelle Cohen there is a housing crisis occurring in NYC, particularly in housing affordability. As the coronavirus pandemic has disproportionately affected low-income households to date, looking at the income levels of households being evicted can help provide insight into which demographics are most at risk. Topics covered include:
- Analysis of the relationship between income and evictions by zip code
- Creating interactive maps with [Plotly Express](https://plotly.com/python/plotly-express/)
- Geocoding from addresses to get missing spatial data

Python and [Jupyter notebooks](https://jupyter.org/) were used for all analysis in this project. [Anaconda](https://www.anaconda.com/) is recommended for installing packages and dependencies for all notebooks. 

## Evictions and Income in NYC
- Notebook: [NYC_Evictions_Income.ipynb](https://github.com/nateswill/Evictions-in-NYC/blob/main/Jupyter_Notebooks/NYC_Evictions_Income.ipynb)
### Dependencies: the following Python libraries are used in this notebook
- pandas
- numpy
- matplotlib
- cenpy
- geopandas

### Data
- ACS household median income data was used from the ACS 2020 5-year estimates. The [cenpy](https://github.com/cenpy-devs/cenpy) library was used to request data directly from the census data API. See the [Census data API documentation](https://www.census.gov/data/developers/guidance/api-user-guide.Overview.html) for more info.
- [Evictions](https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4) data from NYC Open Data. This dataset provides evictions in NYC from January 2017 - present.
- [Modified Zip Code Tabulation Areas (MODZCTA)](https://data.cityofnewyork.us/Health/Modified-Zip-Code-Tabulation-Areas-MODZCTA-/pri4-ifjk) was used to merge in NYC zip code geometries for mapping evictions and income data.

### Story
Is there a correlation between income and evictions?

First let's take a look at evictions from NYC Open data. The data tracks evictions starting in January 2017. Below is a time series plot of evictions per day from January 2017 until today. There was a steep decline in the spring of 2020 when the eviction moratorium started. Then evictions were close to zero for a few months, until a gradual uptick began in the middle of 2021. Currently evictions are increasing steadily.

![Image](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/evic_time_series.png)

What do cumulative evictions look like in NYC? 

Below is a choropleth plot of evictions to date by zip code.  There are clear differences in evictions across zip codes, with the highest numbers appearing in the Bronx and northeast Brooklyn.

![Images](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/evictions.png)

How does this compare with income? 

In order to compare income to evictions, let's look at a choropleth plot of median incomes by zip code in NYC, using data from the 2020 ACS 5-years estimates. Visually speaking, there appears to be a strong negative correlation between income and evictions by zip code. Zip codes with the highest eviction counts tend to have lower median incomes. This is particularly true for our high eviction zips in the Bronx and Brooklyn, as they have some of the lowest median incomes in the City.

![Image](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/income.png)

## Using Plotly Express and Mapping with NYC Open Data

In this project I explore making maps with the [Python Plotly Express](https://plotly.com/python/plotly-express/) library using jupyter notebooks.  The dataset is [NYC evictions data](https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4) that is publicly available on the NYC Open Data website.  The Plotly Express library is easy to use and has lots of high level interactive features, including automatic hover labels. You can also zoom in and out and click and drag the map to move it. I also included a geocoding notebook where I geocoded the evictions addresses using the Nominatum library and OpenStreetMap. Check out the notebooks for details!

## Choropleth Plot
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/choropleth.JPG)

## Heatmap
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/heatmap.JPG)

## Scatter Plot
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/scatterplot.JPG)
