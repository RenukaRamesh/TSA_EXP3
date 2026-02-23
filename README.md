# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
### Date: 23.02.2026
### Name: Ramesh Renuka
### Reg.no: 212223240136
### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### SOFTWARE REQUIRED:
Google Colab
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
data = pd.read_csv('/content/retail_sales_dataset.csv')
data.index = pd.to_datetime(data.index)
daily_counts = data.resample('D').size()

N = len(daily_counts)
lags = range(min(35, N // 2)) 
autocorr_values = []
time_series_data = daily_counts
mean_data = np.mean(time_series_data)
variance_data = np.var(time_series_data)

normalized_data = (time_series_data - mean_data) / np.sqrt(variance_data) if variance_data != 0 else (time_series_data - mean_data)
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:

        auto_cov = np.sum((time_series_data[:-lag] - mean_data) * (time_series_data[lag:] - mean_data)) / N
 
        autocorr_values.append(auto_cov / variance_data if variance_data != 0 else 0)

plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)
plt.title('Autocorrelation of Daily Entry Counts')
plt.xlabel('Lag (Days)')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```
### OUTPUT:
<img width="903" height="564" alt="image" src="https://github.com/user-attachments/assets/ea58d3df-7485-4af7-bca9-7773018c50c9" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
