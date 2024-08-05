# **Seoul-Bike-Sharing-demand-prediction - Regressor**
Addressed the problem of predicting bike sharing demand in Seoul city by converting it  into a regression problem by identifying and quantifying the relationships between bike  bookings and features such as hours, holidays, weekdays, rainfall, and humidity.

## **Problem Statement**
Seoul bike sharing demand prediction project is to develop a reliable model that accurately forecasts the demand for bike rentals in the city. By analyzing historical data on bike usage and incorporating factors such as time, weather conditions, and special events, the project aims to anticipate fluctuations in demand across different time periods and locations. The goal is to optimize the allocation of bikes within the bike sharing system(location wise), ensuring that sufficient resources are available at high-demand locations and times while minimizing operational costs and excess inventory. Ultimately, the project seeks to improve the overall efficiency and usability of the bike sharing system, enhancing user satisfaction and promoting sustainable urban transportation.

## **Dataset Variable Description**
**Date** - day/month/year of booking

**Rented bike count** - Count of bikes rented for each hour

**Hour** - Hour of day

**Temperature** - Temperature in celsius

**Humidity(%)** - relative humidity at the time of bike rental, affecting comfort levels of bike sharing.

**Wind speed (m/s)** - Wind speed in meters/second

**Visibility (10m)** - Visibility in meters at the time of bike rental, influencing safety.

**Dew point temperature (C)** - Indicating level of moisture in air.

**Solar radiation (mj/m2)** - indicating intensity of sunlight.

**Rainfall (mm)** - amount of rainfall in mm at the time of bike rental.

**Snowfall (cm)** - amount of snowfall in centimeters at the time of bike rental.

**Seasons** - spring/summer/autumn/winter  as the time of bike rental, capturing seasonal variations in biking behaviour.


**Holiday** - indicating wheather its holiday or not holiday.

**Functioning day** - indiacting wheather bike sharing system is in operational or not.


## **Data wrangling steps:**
- Converting Date column from object to datetime Date column was in object data type converted to datetime format.
- Creating new variables of weekday, day, month, year variables from date variable From Date variable extracting weekday, day, month, year for exploratory data analysis
- Removing Date feature from df dataframe Since we have extracted weekday, day, month, year from Date variable, Dropping Date variable from the dataframe to reduce data redundancy.

## **Feature engineering:**
- Performed One-hot encoding it preserves all the information present in the categorical variable without imposing any ordinality or hierarchy and retaining distinctiveness of each catgeory. implemented variavles - Holiday, Functional day, seasons, weekday.
- From heatmap we found that Temperature(°C) and Dew point temperature(°C) has high correlation of 0.91. To identify individual contribution to predict target variable Variance inflation factor is performed Dew point temperature VIF was 118 and temperature VIF 90.13 after removing Dew point temperature feature VIF of temperature has decreased to 5.06 which is allowable.





















