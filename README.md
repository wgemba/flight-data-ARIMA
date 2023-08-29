# Analysis and Forecasting of Flight Demand using an ARIMA Modelling  
## Abstract
My goal for this project was to use Python to analyze data about flights in order to answer critical questions that may concern several stakeholders in the airline industry such as airline companies, airports, and passengers. I downloaded data which I analyzed to identify flight patterns. The patterns my program identified allowed me to create historical models that showed key information on flight demand by location as well as demand by the time of year. I then used ARIMA a time series forecasting model to forecast predictions of future flight patterns based on the actuals that I analyzed. Finally, I validated my model by comparing the results from the python program to the actuals of the data we used.

## About the dataset
The date was retrieved from a publicly available file on Kaggle. The time period ranges from 2016 to 2018 and includes 694,917 data points. The consists of several variables, including date, origin city, region, country, airport, destination city, and demand.

## Model Methodlogy - What is ARIMA
ARIMA is a popular time-series forecasting model. ARIMA is an acronym that stands for AutoRegressive Integrated Moving Average. In other words the model can be broken down into three parts: 
- Autoregression: The existance of a dependent relationship between an observation and some number of lagged observations.
- Integrated: The use of differencing of raw observations (e.g. subtracting an observation from an observation at the previous time step) in order to make the time series stationary.
- Moving Average: The use of the dependency between an observation and a residual error from a moving average model is applied to lagged observations.

### Stationarity
As is implied by the integrated aspect of ARIMA, data must be stationary for ARIMA to work. Stationarity is defined by a constant state of mean and variance over time. One of the major draw-backs of the ARIMA model is that it cannot handle any non-stationarity. Thus the first thing that must be done is to determine whether the data is infact stationary. If not, then a number of layers of difference must be performed to create a stationary dataset for forecasting. It so happens, that the raw data itself is stationary, this 0 orders of differencing is requried.

### Model and Parameters
In this project I utilized the ARIMA model from the Python 'statsmodels' library. The ARIMA functuon taked three parameters: p,d, and q. These parameters are defined as follows:

- p: The number of lag observations included in the model, also called the lag order.
- d: The number of times that the raw observations are differenced, also called the degree of differencing.
- q: The size of the moving average window, also called the order of moving average.

P is determined by plotting a partial autocorrelation function and identifying the lag that is the most statistically significant. 

D can be determined by perfroming an Augmented Dickey-Fuller test (ADF test), which calculates the p-value and compares it with a threshold value or significance level of 0.05. The number of orders of differencing corresponds to the number of differencing required for the p-value to fall below the threhold of 0.05. Alternatively, the number of differencing orders can be determined by the 'ndiffs' function from the 'pmdarima' library. 

Q is determined by ploting the autocorrelation function and counting the number of lags that fall outside of the statistical threshold.
