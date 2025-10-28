# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 18/08/2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('/mnt/data/GoogleStockPrices.csv')

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['Close'] = data['Close'].astype(float)

data['Close_diff'] = data['Close'] - data['Close'].shift(1)

result = seasonal_decompose(data['Close'].dropna(), model='additive', period=30)
data['Close_resid'] = result.resid

data['Close_log'] = np.log(data['Close'])
data['Close_log_diff'] = data['Close_log'] - data['Close_log'].shift(1)

result_log = seasonal_decompose(data['Close_log'].dropna(), model='additive', period=30)
data['Close_log_resid'] = result_log.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Close'], label='Original')
plt.legend(loc='best')
plt.title('Original Google Stock Price')
plt.xlabel('Date')
plt.ylabel('Close Price')

plt.subplot(6, 1, 2)
plt.plot(data['Close_diff'], label='Regular Difference', color='orange')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('ΔClose')

plt.subplot(6, 1, 3)
plt.plot(data['Close_resid'], label='Seasonal Adjustment', color='green')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Residual')

plt.subplot(6, 1, 4)
plt.plot(data['Close_log'], label='Log Transformation', color='purple')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Close)')

plt.subplot(6, 1, 5)
plt.plot(data['Close_log_diff'], label='Log Transformation + Differencing', color='brown')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('ΔLog(Close)')

plt.subplot(6, 1, 6)
plt.plot(data['Close_log_resid'], label='Log Transformation + Seasonal Adjustment', color='red')
plt.legend(loc='best')
plt.title('Log Transformation + Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Residual')

plt.tight_layout()
plt.show()

data[['Close', 'Close_diff', 'Close_log', 'Close_log_diff']].plot(
    subplots=True, figsize=(12, 10), title=['Original', 'Diff', 'Log', 'Log Diff'])
plt.tight_layout()
plt.show()

```

### OUTPUT:


REGULAR DIFFERENCING:
<img width="1019" height="338" alt="image" src="https://github.com/user-attachments/assets/37dbd7b2-4178-421a-ba0e-b91c3a6ff936" />


SEASONAL ADJUSTMENT:
<img width="1015" height="340" alt="image" src="https://github.com/user-attachments/assets/0dc9eda9-506a-4e45-967e-345980ac32ca" />


LOG TRANSFORMATION:
<img width="1053" height="326" alt="image" src="https://github.com/user-attachments/assets/a793916a-7416-4b78-9bec-c821b43420a5" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
