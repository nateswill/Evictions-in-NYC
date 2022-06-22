# Evictions in New York City

## Table of contents
- [Introduction](#Introduction)
- [Evictions and Income in NYC](#Evictions-and-Income-in-NYC)
- [Mapping with Plotly Express](#Mapping-with-Plotly-Express)
- [Geocoding with Nominatum and OpenStreetMap](#Geocoding-with-Nominatum-and-OpenStreetMap)

## Introduction
This is an exploratory data analysis of Evictions in NYC. As explained in this [article](https://www.6sqft.com/new-survey-highlights-nycs-rental-housing-crisis-showing-few-affordable-apartments-available/) by Michelle Cohen there is a housing crisis occurring in NYC, particularly in housing affordability. As the coronavirus pandemic has disproportionately affected low-income households to date, looking at the income levels of households being evicted can help provide insight into which demographics are most at risk. Topics covered include:
- Analysis of the relationship between income and evictions by zip code
- Creating interactive maps with [Plotly Express](https://plotly.com/python/plotly-express/)
- Geocoding from addresses to get missing spatial data

Python and [Jupyter notebooks](https://jupyter.org/) were used for all analysis in this project. [Anaconda](https://www.anaconda.com/) is recommended for installing packages and dependencies for all notebooks. 

## Data
- ACS household median income data was used from the ACS 2020 5-year estimates. The [cenpy](https://github.com/cenpy-devs/cenpy) library was used to request data directly from the census data API. See the [Census data API documentation](https://www.census.gov/data/developers/guidance/api-user-guide.Overview.html) for more info.
- [Evictions](https://data.cityofnewyork.us/City-Government/Evictions/6z8x-wfk4) data from NYC Open Data. This dataset provides evictions in NYC from January 2017 - present.
- [Modified Zip Code Tabulation Areas (MODZCTA)](https://data.cityofnewyork.us/Health/Modified-Zip-Code-Tabulation-Areas-MODZCTA-/pri4-ifjk) was used to merge in NYC zip code geometries for mapping evictions and income data.

## Evictions and Income in NYC
- Notebook: [NYC_Evictions_Income.ipynb](https://github.com/nateswill/Evictions-in-NYC/blob/main/Jupyter_Notebooks/NYC_Evictions_Income.ipynb)

### Dependencies: the following Python libraries are used in this notebook
- pandas
- numpy
- matplotlib
- cenpy
- geopandas

### Story
Is there a correlation between income and evictions?

First let's take a look at evictions from NYC Open data. The data tracks evictions starting in January 2017. Below is a time series plot of evictions per day from January 2017 until today. There was a steep decline in the spring of 2020 when the eviction moratorium started. Then evictions were close to zero for a few months, until a gradual uptick began in the middle of 2021. Currently evictions are increasing steadily.

![Image](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/evic_time_series.png)

What do cumulative evictions look like in NYC? 

Below is a choropleth plot of cumulative evictions to date by zip code.  There are clear differences in evictions across zip codes, with the highest numbers appearing in the Bronx and northeast Brooklyn. For people who are familiar with New York City, it is clear that areas with higher eviction counts are also in lower-income areas of the City.

![Images](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/evictions.png)

How can we compare evictions and income more precisely?

In order to compare income to evictions, let's look at a choropleth plot of median incomes by zip code in NYC, using data from the 2020 ACS 5-years estimates. Visually speaking, there appears to be a strong negative correlation between income and evictions by zip code. Zip codes with the highest eviction counts tend to have lower median incomes. This is particularly true for our high eviction zips in the Bronx and Brooklyn, as they have some of the lowest median incomes in the City.

![Image](https://github.com/nateswill/Evictions-in-NYC/blob/main/images/income.png)

Is there a strong correlation between evictions and income by zip code?

The correlation coefficient between eviction and income by zip code was -0.56 (as of today, 6/20/22). This indicates that there is a negative correlation, however strong correlation is typically of a magnitude larger than 0.7 (in this case -0.7). Next, I would like to normalize the evictions counts by zip code population size. This will increase the accuracy of our analysis and may provide a stronger correlation.

Conclusion: After analyzing the relationship between income and zip code in NYC, both visually and quantitatively, there does appear to be a negative correlation. Low-income zip codes tend to have a larger number of evictions. As gentrification, inflation, housing speculation, and Covid are exacerbating an ongoing housing crisis in NYC, it is critical that we examine how these issues are effecting housing insecurity.

## Mapping with Plotly Express
- Notebook: [Mapping_with_Plotly_Express](https://github.com/nateswill/Evictions-in-NYC/blob/main/Jupyter_Notebooks/Mapping_with_Plotly_Express.ipynb)

### Dependencies
- pandas
- numpy
- matplotlib
- urllib
- json
- plotly

### Background
Just for fun - I made maps with the [Python Plotly Express](https://plotly.com/python/plotly-express/) library. The plotly express library is easy to use and has lots of high level interactive features, similar to what you would find in mapping software like ArcGIS or QGIS. The maps use a lot of memory to run in Jupyter, so I loaded them to github as raw code. Download the notebook and run to get the full interactive experience! Below are images of a choropleth, heatmap and scatterplot of NYC evictions data.

## Choropleth Plot
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/choropleth.JPG)

## Heatmap
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/heatmap.JPG)

## Scatter Plot
![Image](https://github.com/nateswill/Mapping_NYC_Evictions_Data/blob/main/images/scatterplot.JPG)

## Geocoding with Nominatum and OpenStreetMap
- Notebook: [Geocode_Evictions_data](https://github.com/nateswill/Evictions-in-NYC/blob/main/Jupyter_Notebooks/Geocode_Evictions_data.ipynb)

### Dependencies
- pandas
- numpy
- geopandas
- geopy
- time

### Background
This notebook was used to geocode the addresses in the NYC Evictions data, in order to get points to plot in the heatmap and scatterplot with plotly express. This notebook contains a link to instructions on how to set up a [virtual environment to run geopandas](https://medium.com/@sourav_raj/ultimate-easiest-way-to-install-geopandas-on-windows-add-to-jupyter-notebook-which-will-a4b11223f4f2). This can also be a helpful guide for folks who are learning how to create environments with Anaconda.

Using this [article](https://towardsdatascience.com/geocode-with-python-161ec1e62b89) as a guide, the evictions dataset was geocoded with the Nominatum library and OpenStreetMap. *Update 2022*: The NYC Evictions dataset has changed, and most of the data is now geocoded. There are still ~6K rows without geocoding, so folks can still contribute their geocoded data to the dataset!
As there was only addresses in the NYC Evictions data originally, I created this notebook to geocode the addresses for the heatmap and scatterplot with plotly express. 
