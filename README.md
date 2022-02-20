# World-Weather-Analysis


# Task
We are tasked with collecting and analyzing weather data for 500 or more cities worldwide. 

# Purpose

PlanMyTrip is a top travel technology company that specializes in the internet-related services in the hotel and lodging industries. The company present data for customers via the search page, which they can filter based on their preferred travel criteria to find their "ideal" hotel anywhere in the world. The "ideal" hotel is narrowed down to:
1) within a given range of latitude and longitute, and 
2) that provided the right kind of weather for the client. 

# Method
Perfrom requests on the OpenWeather API and retreieve the JSON weather data from these cities. The weather data in real time for 500 or more unique cities around the world will be added to a Pandas DataFrame, where we will use the matplotlib to create the series of scatterplots to show the relationship and a variety of weather parameters. Using linear regression, we predict the best time of year to plan their vacation. 

Using API we will collect weather data for over 500 cities around the world. We will analyze the data using Pandas and plot the data using Matplotlib libarary and Google maps API. Perform statistical analysis using SciPy libarary. The end result will be a series of plots that visually and statistically show the relationship between latitude and a variety of weather parameters.


The algorithm developed in this project can be resuded to get many more cities. 


1. Collect the Data
- Use the NumPy module to generate more than 1,500 random latitudes and longitudes.
- Use the citipy module to list the nearest city to the latitudes and longitudes. 
- Use the OpenWeatherMap API to request the current weather and data from each unique city in your list. 
- Parse the JSON data from the API request. 
- Collect the following data from the JSON file and add it to a DataFrame:
 - City, country, and date
 - Latitude and longitude
 - Maximum temperature
 - Humidity
 - Couldiness
 - Wind spee

 2. Exploratory Analysis with Visualization
- Create scatter plots
- Determine the correlations
- Create a series of heatmaps usinof the weather data o
    for the following:
    - Latitude vs temperature 
    - Latitude vs humidity 
    - Latitude vs cloudiness
    - Latitude vs wind speed

3. Visualize Travel Data
Create a heatmap with pop-up markers that can display information on specific cities based on a customer's travel preferences. Complete these steps:
    - Filter the Pandas DataFrame based on user inputs for a minimum and maximum temperature. 
    - Create a heatmap for the new DataFrame. 
    - Find a hotel from the cities's coordinates using Google's Maps and Places API, and Search Nearby feature. 
    - Store the name of the first hotel in the DataFrame. 
    - Add pop-up markers to the heatmap that display information about the city, current maximum temperature, and a hotel in the city.


# Setting the limit on data collection
70% of Earth is covered by water and the rest with land. So, pulling geographic coordinates over water-covered areas might not be close to the city, especially if in the middle of an ocean. 

So, seven continents comprise 30% of the land on Earth. Some areas can be unihabitable or sparsely populated due to extreme climate and/or terrain (e.g., Sahara, Siberia, the Himalayas, and western areas of the United States).

When generating random latitudes and longitudes, it is important to ensure that coordinates are fairly distributed around the world. The algoritm will pull random latitudes and longitudes between the low and high values of coordinates. 

The format of coordinates must be floating-point decimals as angular units of degrees, minutes, and seconds can be represented as a decimal number. 

500 cities divided 0.3 (30% of land) is 1,500 latitudes and longitudes. 


City, country, and date
Latitude and longitude
Maximum temperature
Humidity
Cloudiness
Wind speed

# Preliminary Exploratory Analysis by Visualizing Data

## City Latitude vs. Maximum Temperature
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs%20Max%20Temp.png)

The above scatter plot does not show a single linear pattern. However, we can notice linear patters if we divide the data in two parts - Northern and Southern hemispheres. And, in each part, the maximum temperatures tends to increase as the latitude is closer to the equator. The temperature tends to decrease as the latitude is farther from the equator. 

## City Latitude vs. % of Humidity 
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Humidity.png)

The scatter plot does not show any definitive pattern. However, we can see a very weak negative association in each hemisphere. 

## City Latitude vs. Cloudiness

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Cloudiness.png)

The scatter plot does not show any definitive pattern.

## City Latitude vs. Wind Speed

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Wind%20Speed.png)

The scatter plot does not show any definitive pattern.

# Regression Analysis on Each Northern and Southern Hemispheres

Conducting a regression analysis can confirm our preliminary findings above.

## City Latitude vs. Maximum Temperature
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Max%20Temp_North.png)
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Max%20Temp_South.png)

Now, we can see that, indeed, the regression confirms a strong negative association between the city latitude and maximum temperature in the Northen Hemishpere. In the Southern Hemispher, the relationship is weaker and positive. 

So, the latitude might be used to predict the maximum temperature. However, it is important to note that to make any causual inferences, we need to investigate other factors affecting the maximum temperature. 


## City Latitude vs. % of Humidity 
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Humidity_North.png)
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/weather_data/Latitude%20vs.%20Humidity_South.png)

There is a weak association between the city latitude and humidity in each hemisphere. So, the humidity might not be well-predictable by the change in the latitude. 

## City Latitude vs. Cloudiness

![]()
![]()

The correlation between the city latitude and cloudiness is very low and slightly positive. So, the cloudiness might not be well-predictable by the change in the latitude. 

## City Latitude vs. Wind Speed

![]()
![]()
There association between the latitude and wind Speed is almost non-existant with a close to zero slope. So, the wind cannot be predictable by changes in latitude. 