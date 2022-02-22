# World-Weather-Analysis

# Overview of the Project 

## Background

PlanMyTrip is a top travel technology company that specializes in the internet-related services in the hotel and lodging industries. 

## Purpose 
The purpose of this project is to collect and analyze weather data for more than 500 cities around the world. Furthemore, we are tasked with helping PlanMyTrip with presenting the weather data for customers via the search page, which they can filter based on their preferred travel criteria to find their "ideal" hotel anywhere in the world. The "ideal" hotel is narrowed down to:
1) within a given range of latitude and longitute, and 
2) that provided the right kind of weather for the client. 

The algorithm developed in this project can be reuded to get many more cities. 

# Methodology and Analysis

1. Setting the limit on data collection. 2000 random combinations of latitudes and longitudes were generated using the NumPy module. 

When generating random latitudes and longitudes, it is important to ensure that coordinates are fairly distributed around the world. The algoritm will pull random latitudes and longitudes between the low and high values of coordinates. 

The format of coordinates must be floating-point decimals as angular units of degrees, minutes, and seconds can be represented as a decimal number. 

2. Corresponding cities were found for these 2000 coordinates using the CitiPy module. However, only 757 unique cities were matched to 2000 coordinates as there were duplicated pairs in the generated coordinates. 
3. A request was made on the OpenWeather API and retreieve the current weather data for eqach unique city in the list in the JSON format. 
4. The weather data in real time was found for 686 cities out of 757 generated cities around the world were collected from the JSON file and added to a Pandas DataFrame with the following:
    - City, country, and date
    - Latitude and longitude
    - Maximum temperature
    - Humidity
    - Couldiness
    - Wind speed
    - Current Weather Description (e.g., clouds, fog, light rain, clear sky)
![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Weather_Database_686%20cities.png)
5. **Exloratory Analysis** was done using matplotlib to create the series of scatterplots to show the relationship and a variety of weather parameters. Using linear regression, we predict the best time of year to plan their vacation. 

**City Latitude vs. Maximum Temperature**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Latitude%20vs%20Max%20Temp.png)

The above scatter plot does not show a single linear pattern. However, we can notice linear patters if we divide the data in two parts - Northern and Southern hemispheres. And, in each part, the maximum temperatures tends to increase as the latitude is closer to the equator. The temperature tends to decrease as the latitude is farther from the equator. 

**City Latitude vs. % of Humidity**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Latitude%20vs.%20Humidity.png)

The scatter plot does not show any definitive pattern. However, we can see a very weak negative association in each hemisphere. 

**City Latitude vs. Cloudiness**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Latitude%20vs.%20Cloudiness.png)

The scatter plot does not show any definitive pattern.

**City Latitude vs. Wind Speed**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Latitude%20vs.%20Wind%20Speed.png)

The scatter plot does not show any definitive pattern.

6. **Regression Analysis on Northern and Southern Hemispheres** was done to confirm our preliminary findings above using the SciPy library.

**City Latitude vs. Maximum Temperature**

![]()

<img src="https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_MaxTemp_North.png" width="250" height="250">

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_MaxTemp_South.png)

Now, we can see that, indeed, the regression confirms a strong negative association between the city latitude and maximum temperature in the Northen Hemishpere. In the Southern Hemispher, the relationship is weaker and positive. 

So, the latitude might be used to predict the maximum temperature. However, it is important to note that to make any causual inferences, we need to investigate other factors affecting the maximum temperature. 


**City Latitude vs. % of Humidity**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_Humidity_North.png)

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_Humidity_South.png)

There is a weak association between the city latitude and humidity in each hemisphere. So, the humidity might not be well-predictable by the change in the latitude. 

**City Latitude vs. Cloudiness**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_Cloudiness_North.png)

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_Cloudiness_South.png)

The correlation between the city latitude and cloudiness is very low and slightly positive. So, the cloudiness might not be well-predictable by the change in the latitude. 

**City Latitude vs. Wind Speed**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_WindSpeed_North.png)

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Analysis/Lin_Regression_WindSpeed_South.png)


There association between the latitude and wind speed is almost non-existant with a close to zero slope. So, the wind cannot be predictable by changes in latitude. 

7. **Heatmaps** were created for all 729 cities to display the density of each weather parameter. 

**Maximum Temperature Heatmap**
Google heatmaps do not plot negative numbers. Since the generated weather data has negative values for maximum temperaturesm, only positive ones were selected. Now the number of cities has decreased to 660 cities with only positive maximum temperatures. 

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Heatmaps/Max%20Temp%20Heatmap.png)

**Humidity Heatmap**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Heatmaps/Humidity%20Heatmap.png)

**Cloudiness Heatmap**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Heatmaps/Cloudiness%20Heatmap.png)

**Wind Speed Heatmap**

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Weather_Database/Heatmaps/Wind%20Speed%20Heatmap.png)


8. **A Vacation Search Map** was created with pop-up markers that can display information on specific cities based on a customer's travel preferences. The following steps were completed:
    - The Pandas DataFrame was filtered based on user inputs for a minimum and maximum temperature. As an example, a minimum temperature of 75 and maximum temperature of 90 were inputted, which returned 198 cities. 
    - Next, the nearby hotels were found from the cities's coordinates using Google's Maps and Places API, and Search Nearby feature. The name of the first hotel (default is rank by prominence) for each city was stored. 
    - The heatmap with pop-up markers was created that can display information about the city, the most popular hotel, current maximum temperature, and current weather description. 

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Vacation_Search/Vacation_Search_Map.png)

9. **A Travel Itinerary Map** was created to show an example route between four cities chosen from the customer's chosen travel destinations.  

The example destinations are in Mexico:

- Vacation Start: Coahuayana
- Vacation End: Coahuayana
- Vacation Stop1: Acapulco
- Vacation Stop2: Puerto Escondido
- Vacation Stop3: Huatulco

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Vacation_Itinerary/Maps/Example%20Route%20copy.png)

![](https://github.com/Aigerim-Zh/World-Weather-Analysis/blob/main/Vacation_Itinerary/Maps/Map%20with%20Markers%20copy.png)

