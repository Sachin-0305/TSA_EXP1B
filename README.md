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
data=pd.read_csv('/content/BMW_Car_Sales_Classification.csv')
data.head()

data['Year']=pd.to_datetime(data['Year'], format='%Y')
data.set_index('Year',inplace=True)

data['Sales_diff']=data['Sales_Volume']-data['Sales_Volume'].shift(1)

result = seasonal_decompose(data['Sales_Volume'], model='additive', period=12)
data['Sales_diff']=result.resid

data['Sales_Volume_log'] = np.log(data['Sales_Volume'])
data['Sales_Volume_log_diff']=data['Sales_Volume_log']-data['Sales_Volume_log'].shift(1)

result = seasonal_decompose(data['Sales_Volume_log'].dropna(), model='additive',period=12)
data['Sales_Volume_log_diff']=result.resid

plt.figure(figsize=(16, 16))


plt.plot(data['Sales_Volume'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Sales_Volume')

plt.plot(data['Sales_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced of Sales')

plt.plot(data['Sales_Volume_log_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted Sales')

plt.plot(data['Sales_Volume_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Sales)')

plt.plot(data['Sales_Volume_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(Sales))')

plt.plot(data['Sales_Volume_log_diff'], label='Log Transformation and regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Sales)))')

plt.tight_layout()
plt.show()

data.plot(kind='line')
```

### OUTPUT:


REGULAR DIFFERENCING:
<img width="903" height="610" alt="image" src="https://github.com/user-attachments/assets/343c91f5-ac56-410c-9340-e3984b57c763" />


SEASONAL ADJUSTMENT:
<img width="811" height="612" alt="image" src="https://github.com/user-attachments/assets/00d910f2-dd9f-4e61-82d8-0c5f3218a486" />


LOG TRANSFORMATION:
<img width="761" height="589" alt="image" src="https://github.com/user-attachments/assets/24405bb9-8ed2-45d1-9ade-58541dbf4e89" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
