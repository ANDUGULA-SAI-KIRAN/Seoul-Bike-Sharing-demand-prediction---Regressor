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

## **ML Model implementation:**
![image](https://github.com/user-attachments/assets/ad4a2452-b6d6-41ab-8e7c-f3451b24336b)

#### **Linear regression model y_test vs y_predicted visualisation**
![image](https://github.com/user-attachments/assets/3067b122-9afe-4700-9b7f-10b094552a4d)


#### **Randomforest model y_test vs y_predicted visualisation**
![image](https://github.com/user-attachments/assets/7cba5bac-d4cf-4893-8621-af8652a9f385)

#### **Xtreme gradient boosting model y_test vs y_predicted visualisation**
![image](https://github.com/user-attachments/assets/9fba0e6c-faad-48f2-b487-f9c9a182092a)


## **Randomforest Hyperparameter tuning** 

Number of trees in random forest
n_estimators = [int(x) for x in np.linspace(start = 200, stop = 2000, num = 10)]

Number of features to consider at every split
max_features = ['auto','sqrt']

Maximum number of levels/splits allowed in each decision tree
max_depth = [int(x) for x in np.linspace(10,120,num=12)]

Minimum number of samples required to split a node
min_samples_split = [2,5,10]

Minimum number of samples required at each leaf node
min_samples_leaf = [1,2,4]

Method of selecting samples for training each tree
bootstrap = [True, False]

random_grid = {'n_estimators': n_estimators,
                'max_features': max_features,
                'max_depth' : max_depth,
                'min_samples_split': min_samples_split,
                'min_samples_leaf': min_samples_leaf,
                'bootstrap' : bootstrap}

#### **RandomForest Best params**

'n_estimators': 400,
'min_samples_split': 2,
'min_samples_leaf': 1,
'max_features': 'auto',
'max_depth': 60,
'bootstrap': True

**Evaluation metrics**
'Model': 'Random Forest Regression_ randomised CV',
'MSE': 32181.985,
'RMSE': 179.393,
'MAE': 101.686,
'r2': 0.923




## **XGboost Hyperparameter tuning** 
params = {'max_depth': [3,5,7,9,15,20],
          'learning_rate': [0.01, 0.1, 0.2 ,0.3],
          'subsample': np.arange(0.5, 1, 0.1),
          'colsample_bytree':np.arange(0.4,1,0.1),
          'colsample_bylevel':np.arange(0.4,1,0.1),
          'n_estimators': [100, 500 , 1000]
          }
xgbr = XGBRegressor(seed = 20)
xgbr_random = RandomizedSearchCV(estimator = xgbr,
                                 param_distributions = params,
                                 scoring = 'neg_mean_squared_error',
                                 n_iter = 25,
                                 cv = 5,
                                 verbose = 1)

#### **XGboost Best params**

'subsample': 0.8999999999999999,
'n_estimators': 500,
'max_depth': 7,
'learning_rate': 0.1,
'colsample_bytree': 0.8999999999999999,
'colsample_bylevel': 0.7999999999999999}

**Evaluation metrics**

'Model': 'XGB Regressor randomised CV',
'MSE': 19620.848,
'RMSE': 140.074,
'MAE': 78.918,
'r2': 0.953}

## **Model improvement after hyperparameter tuning:**

- For XGboost regressor before tuning model r squared values was 0.938 after hyperparameter tuning r squared values is increased to 0.951.

- Increased accuracy: Model can now predict bike demand with slightly greater precision.

- Better generalization: The tuning process might have helped the model generalize better to unseen data.

- A small improvement in R-squared can be significant in real-world applications. Here 0.013 improvement translates to explaining an even greater proportion of the variance in bike demand.

## **Feature importance of XGBR_model:**

![image](https://github.com/user-attachments/assets/0f986809-11ef-4146-8b80-4b53cb267a0f)


## **Conclusions:**

A linear regression model was developed to forecast bike rental demand. By analyzing historical data and incorporating features such as hours, holidays, weekdays, rainfall, and humidity, we were able to optimize resource allocation within the bike-sharing system. After extensive data wrangling and feature engineering, implemented and tuned multiple regression models. The Random Forest model achieved an R² of 0.923 with an MSE of 32,181.985, an RMSE of 179.393, and an MAE of 101.686. The XGBoost model, after hyperparameter tuning, achieved an R² of 0.953 with an MSE of 19,620.848, an RMSE of 140.074, and an MAE of 78.918. These improvements in model performance are expected to enhance the overall efficiency and usability of Seoul's bike-sharing system, ensuring better bike availability at high-demand locations and times, reducing operational costs, and promoting sustainable urban transportation.

















