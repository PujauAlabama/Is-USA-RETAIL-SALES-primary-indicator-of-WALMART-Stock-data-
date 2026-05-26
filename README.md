# Is USA RETAIL SALES primary indicator of WALMART Stock data?

## Summary
Here I have tried to address whether the USA Retail Sales data is
the best indicator of WMT or not. The general methodology goes as follows.
After downloading the data, I have converted the monthly retail sales data to
quarterly data to match frequency of that of WMT data. Other way to approach
it would be to convert quarterly WMT to data monthly data using Kalman filter.
But as that would be incorporating more error due to interpolation, I planned
to go ahead with Quarterly data. Firstly , I have checked the Cointegration
test to confirm long term stationarity, which would be equivalent to regression
here. But the correlation parameter is too low to validate the dependency.
Hence, I switched for checking the dependency incorporating short term effects
using lag parameters in Granger Causality test. Though the indicator performs
better compared to baseline, the dependency is yet not confirmed because of
the small value of the correlation parameter. Hence dependency (if exists after
this point) can be addressed via volatility modeling and seasonal dependence.
For this I have incorporated SARIMAX rolling window method with 1 day
window. After I obtained the residual term, GARCH model have been employed
to get confidence intervals (95 percent) from the residual. And Retail Sales
contribution has been found in seasonal effects of WMT.
## Data Source
For downloading USA Retail Sales data I have used FRED-API website and
Walmart WMT stock data have been fetched from yfinance. As the frequencies
don’t match for both, I have transformed the Retail sales data from monthly to
quarterly using SUM method.

## Data Analysis
### Co-Integration Check
To figure out long term dependency between WMT and Retail Sales data, cointegration
test has been performed. Though the time-series plots show the
trend pattern are same for both of them, the time-series data are not correlated
(verified from p-value). This confirms that only regression would not be enough
to address the causal effect between these.
### Short-Term Dependency Check via Lag parameters
In this part , I tried to figure out short term dependency using the naive baseline
and auto-regression lag parameters. Though the Stock growth beats the basleine
by 7.37 percent, correlation coefficient .1184 is not that significant to prove
dependency. The Granger causality test lag value increase shows that the pvalues
get worse with higher lag parameter, implying if the depndenct exists ,
the it would be dependent at best on recent data or very small time span of old
data.
### Forecast using SARIMAX -Rolling window method to
check Seasonal Contribution
As previous analysis confirms the dependency of WMT on Retail Sales data
most likely coming from short period small lagged data, I have used SARIMAX
rolling window method, where SARIMAX would be figuring out ARIMA(p,q,d)
and SEASONAL(P,Q,D,S), here I have used log transformation to kill abrupt
changes causing error, and kept S = 4 considering seasonal quarterly effect. AIC
values has been incorporated to find out optimal values of parameters (though
kept d = D = 1 constant throughout, as I have checked for other values giving
more error). Then I have used residual to implement GARCH modeling to have
95 percent confidence interval. The overall mean absolute percentage error is
coming to be 6.74 percent from the model.
4 Conclusion
Though Retail data can’t be expressed as a leading indicator of WMT, it evidently
has seasonal effects that has been confimed from volatility modeling.
