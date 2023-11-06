# Beijing Air Quality
## About
<p align='justify'>Predicting air quality plays a crucial role in safeguarding public health by proactively mitigating exposure to hazardous levels of pollution. The importance of this role becomes even more pronounced for individuals who suffer from respiratory conditions, as they are particularly vulnerable to the risks of unfavorable air quality conditions.</p>

<p align='justify'>According to the <a href=https://www.airnow.gov/aqi/aqi-basics/>US Environmental Protection Agency (EPA)</a> the Air Quality Index (AQI) is divided into 6 categories according to a different level of health concern. These categories of AQI (in ug/m^3) of ozone and particle pollution are as follows:</p></br>

<p align="center">
  <img src="imgs/AQI_Index.jpg" alt="[aqi_index]">
</p></br>

<p align='justify'>We are going to perform multivariate time series forecasting employing deep learning on <a href=https://archive.ics.uci.edu/dataset/381/beijing+pm2+5+data>Beijing US Ambassy Air Quality dataset</a> which consists of 43824 samples of hourly data of different weather conditions and pollution (pm2.5) level collected between January 1st of 2010 and December 31st of 2014 on the US ambassy of Beijing. The dataset has the following three variables: </p>
<ul>
<li><b>No:</b> row number
<li><b>Year:</b> year the data point was captured
<li><b>Month:</b> month the data point was captured
<li><b>Day:</b> day the data point was captured
<li><b>Hour:</b> hour the data point was captured
<li><b>pm2.5:</b> concentration (in ug/m^3) of particulate matter with a circumference of 2.5 microns 
<li><b>DEWP:</b> dew point
<li><b>TEMP:</b> temperature
<li><b>PRES:</b> pressure
<li><b>cbwd:</b> combined wind direction
<li><b>Iws:</b> cumulated wind speed
<li><b>Is:</b> cumulated hours of snow
<li><b>Ir:</b> cumulated hours of rain
</ul>

## Procedure
<p align='justify'>The objective will be to develop an effective model to predict ahead of time the concentration levels of pm2.5 and thus detect potential health risks and raise awareness on it to prevent exposure. The main metric for success we are going to use is the mean absolute error.
The steps will be:
<ol>
<li>Loading and Cleaning Data
<li>Exploring Data (Clean tweets)
<li>Data Preprocessing
<li>Model development
<li>Model evaluation
</ol>
</p>

## Loading & Cleaning the data
<p align='justify'>It seems clear at first look that our dataset needs some cleaning. To begin with, the variables names are a bit confusing the way they are defined right now so we should rename them. Date variables need to be parsed and set as index and variable 'No' serves no real purpose so we will drop it.</p>

<p align='justify'>We confirm there are missing values in the pm2.5 variable as can be seen in the graph below, exactly 2067, we decide to fill these missing values with zeros and let the model interpret them as missing. There are only two null values in the series which are most likely outliers so it will not significantly affect our model to have them set as missing values.</p></br>

<p align="center">
  <img src="imgs/first-1k.png" alt="[first-1k]">
</p></br>

<p align='justify'>Once the date has been parsed and set as index, the columns 'No', 'Year', 'Month', 'Day' and 'Hour' dropped, clearer columns names have been set, missing values set as zero and the first day of data dropped, since it was missing pm2.5 values and we need the initial values start the training of our model, we can move forward to exploring the data</p></br>

## Exploring the data
<p align='justify'>First of all, we are going to define, using libraries like emoji and re, a few functions to clean our dataset such as:
<ul>
<li>strip_all_entities: remove punctuations, links, mentions and \r\n new line characters
<li>clean_hastags: clean hashtags at the end of the sentence, and keep those in the middle of the sentence by removing just the # symbol
<li>filter_char: filter special characters such as & and $ present in some words
<li>remove_mult_spaces: remove multiple spaces
</ul>
</p>
