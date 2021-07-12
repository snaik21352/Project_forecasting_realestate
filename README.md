
# Project - Time Series Analysis of Zillows housing Data. 


#  Data:
**The goal** of this project is to determine 5 zipcodes in the US for investing and then forecast their return rates. 
<br/>Zillow's research data used for this analysis can be found [here](https://www.zillow.com/research/data/). The data contained about 15k zipcodes. In an effort to determine the best real estate markets, zipcodes were filtered  as follows :
* Zip codes with the highest urbanization (top 25%) based on Zillow’s urbanization metric.
* Zip codes that did not depreciate during the great recession (07–08)
* Zip codes that have returned 3 % or more over the past 20 years
* Zip codes that are experiencing an uptrend in appreciation rates for past 2 years.
This resulted in about 100 zip codes as seen below:
![alt text]()
<br/>Furthermore to determine whether the expected return of the investment is worth the degree of volatility,the zipcodes were filtered based on downside risk.The 4th quintile was chosen in this filteration based on the historical returns. This resulted in about 25 zipcodes. Out of these 25 zipcodes the top 10 with highest returns were chosen for forecasting.

The data did not require any major cleaning or pre-processing , the only changes that were  made was to convert the data into date time obejct using pandas to_datetime funtion. Futhermore the data was reshaped from wide to long format using pandas melt funtion .



# Detrending and accessing/chossing parameters for modelling

The data was transformed using log_transform and detrended using first order finite difference which resulted into 5/10 stationary time series. Second order resulted differencing resulted in all time series to be stationary.All The time series had a mild seasonal component and 
Based on the ACF and PACF plots there were several significant MA and QA orders. So the best option was to chose the optimum parameters using auto arima . More info on this can be found here https://alkaline-ml.com/pmdarima/

#  ARIMA Modeling
Using Auto arima parameters , SARIMAX model was chosen along with dynamic forecasting to predict a 5 yr projection of all 10 zipcodes. Overall percent return was calculated as well. 

#  Interpreting Results

Based on 3-5% yearly appreciation we can expect 15-28% overall return in 5 years . Based on the results the 5 best zipcodes are 70806,70808,73069,70810,78753 which on average will return nearly 44% over the next 5 years
. The reason I selected these 5 zipcodes is because they have 1)The residuals show some changing variation over time but they are relatively stationary,This heteroscedasticity will potentially make the prediction interval slightly inaccurate. 2)Residuals are more or less normally distributed. 3)Although there exists some autocorrelation, it is not particularly large and it is unlikely to have any noticeable impact on the forecasts or the prediction intervals.

# Future Work
Out of nearly 15k zipcodes the 3 i have come to chose are from Baton rouge LA which suggests that some external factors did not affect the housing market in these regions compared to others during the recession and they continute to appreciate over 5% per year.So I wanted to see if certain zipcodes can be clustered together based on the underlying geography as an external factor. 2) Also the model preiction can be improved by including other external factors such as mortgage rates, local economy, income , crime etc 3) I would like to also inlcude and analyze rental data as rental income can be a factor in real estate investment.
