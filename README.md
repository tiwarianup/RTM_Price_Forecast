# RTM IEX Price Forecasting using Bagging & Boosting Ensembles

In recent years rapid urbanisation and aggressive electrification programs has resulted in an increase in all India energy (electric power) demand. If we observe the past trends in the data published by the Central Electricity Authority (CEA) of India, it is evident that the energy demand will continue to grow in years to come.
On a macro level, it should not be surprising for a rapidly developing nation like India. But, when we look at the micro level which is the day to day operations of the power system, we can find many potential challenges which call for attention to improve the overall performance and efficiency of the power systems. Predicting Real Time Market (RTM) Prices accurately is one such challenge for a power utility. It is of utmost importance for the nation that power supply is never interrupted and thus every power utility thrives to meet the energy demand of their consumers.
The challenge lies in the fact that the increment or decrement of energy demand is a real time process very similar to the price movement on the stock exchanges. This fluctuation in energy demand is to be anticipated and planned in advance for smooth power system operations. We would not go deep into the actual functioning of these systems, but it is good to know that to fulfill this real time anticipated increment or decrement in demand, a power utility may wish to buy or sell power on the Indian Energy Exchange Platform. If the power demand of the utilities' consumers are not fulfilled, they may have to face unplanned outages resulting in customer dissatisfaction.

**Objective of this Exercise:** To analyze and model publically available data using RandomForest (Bagging) and XGBoost (Boosting) machine learning algorithms to predict Real Time Market (RTM) Prices on Indian Energy Exchange (IEX).

**Methodology Followed:** The methodology followed for this exercise can be summarized as follows:
1. Collecting Real Time Market prices and bids data from IEX website (Not Included)
2. Collecting All India Electricity Load (Demand) from Vidyut Pravah website (Not Included)
3. Compiling the data into a single CSV file for analysis (Not Included)
4. Importing, Inspecting and Cleaning the data
5. Visual Inspection of Data (EDA)
6. Hyperparameter Tuning and Cross Validation in RandomForest and XGBoost
7. Predicting Prices using Best Estimators
8. Visualizing and exporting the final results

Traditionally, Time series data is modelled using statistical approaches such as Exponential Smoothing, ARIMA or SARIMAX models etc. An important peculiarity of time series data is autocorrelation, i.e. the dependency of current value on the past values. Further, a time series data is time stamped which means that there is a chronological order maintained in the data that cannot be directly recognized by machine learning models. Thus, we will use a technique called reduction which is a process to transform the available features to account for the time dependency in the data.

**The notebook associated with this article is divided into 3 sections as following:
1. Visual Inspection of data (EDA) & Feature Engineering
2. Implementing RandomForest for Price Predictions
3. Implementing XGBoost for Price Predictions**

> **Highlights of Section1: Visual Inspection of Data (EDA) & Feature Engineering**

**Adding Weekday and Weekend effect:** Electricity power demand and consequently the prices are generally seasonal in nature. Seasonality means cyclicity of a pattern occurring in data over a short range of time. This occurs due to cyclicity in consumer demand patterns. On weekdays the demand may be more as compared to weekends and this needs to be accounted while modelling the time series data. Thus, we will derive a feature (independent variable) to account for the day of week and we will use this feature later in machine learning models.

**Adding Public Holidays effect:** On account of public holidays, since many industries are shut, an impact of overall electricity load is seen which in turn impacts the prices on exchange. Thus, it will be great to add the effect of these special days. In your own respective regions, this day can be a public holiday or election day etc.
Creating Training and Testing Datasets: Now, we will create train and test datasets. Since, time series data analysis requires us to maintain the chronological order of data, we would not be able to use the shuffled train_test_split function present in sklearn. Thus, we will manually create a train test split based on no of training days and no of prediction blocks. Normally in the Real Time Electricity Market, bids are submitted for two timeblocks and thus, we need to with as much accuracy as possible, predict the two timeblocks ahead forecasts.

**Note:** Another peculiarity that arises with time series data is the train, validation, test data splits may not follow the pattern available in either of the sets especially when the volatility is high in the dataset and volatility in prices is often encountered. Thus, we would like to make our training set as large as possible to contain as much information as possible in the dataset. This can lead to overfitting but after several iterations, here we have chosen to train the model on all the data except for the last 96 blocks which we choose as the test set.

> **Highlights of Section 2: Implementing XGBoost for Price predictions**

**Hyperparameter Tuning for XGBoost using GridSearch CrossValidation:** The following parameter grid used for GridSearchCV is obtained after a few iterations of RandomSearchCV technique. We will use neg_mean_squared_error as the evaluation scoring criteria on the validation sets. The best_estimator_ attribute of the gridsearch instance will give us the fit with best parameters.

**Prediction and Model evaluations using Best XGBoost Estimator:** The best estimator obtained after performing Hyperparameter tuning is used to predict the prices.

> **Highlights of Section 3: Implementing RandomForest for Price predictions**

**Hyperparameter Tuning for RF using GridSearch CrossValidation:** The following parameter grid used for GridSearchCV is obtained after a few iterations of RandomSearchCV technique. We will use neg_mean_squared_error as the evaluation scoring criteria on the validation sets. The best_estimator_ attribute of the gridsearch instance will give us the fit with best parameters.

**Prediction and Model evaluations using Best RF Estimator:** The best estimator obtained after performing Hyperparameter tuning is used to predict the prices.

In the end after performing all of these steps, we export the results to csv files for publishing or further decision processes. In this exercise, we saw how we can apply XGBoost and RandomForest models on Time Series data using a technique called reduction. We then applied data cleaning, data transformation and feature engineering to perform reduction. Then, we trained the train sets on both the ML algorithms by performing Hyperparameter tuning and cross validation. Finally, we evaluated the performance of the best estimators on the test set. Both the algorithms gave **~85% accuracy** on test sets.

**Next Steps:** If you wish to extend this exercise, you may wish to model the generator outages, weather impacts on electricity demand, volatility analysis of prices etc. to further improve the performance of these models.



