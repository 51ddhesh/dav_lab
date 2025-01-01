# Experiment 1
#### **Problem :** 
Consider a dataset such as finance, education, marketing, healthcare etc. Load, inspect, and 
store data in various formats like CSV, Excel, JSON, and SQL using Pandas. Clean and prepare 
data by handling missing values, duplicates, normalization, and encoding categorical data. <br>

<br>1. Import the necessary libraries
```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
```
<br>2. Load the Data
```python
file_path = 'Heart.csv'
df = pd.read_csv(file_path)
```
<br>3. Inspect Data:
   - Data Info
   - Data Statistics
   - 5 rows
```python
df.info()
```
```python
df.describe()
```
```python
df.head()
``` 
<br>4. Convert data to different forms like .xlsx, .json, .sql.
```python
df.to_excel('dataset.xlsx', index = False)
```
```python
df.to_json('dataset.json', orient = 'records', indent = 2)
```
```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')
df.to_sql('dataset', con = engine, index = False, if_exists = 'replace')
```
<br>5. Reload data to verify
```python
df_excel = pd.read_excel('dataset.xlsx')
```
```python
df_json = pd.read_json('dataset.json')
```
```python
df_sql = pd.read_sql('dataset', con = engine)
```
<br>6. Data Cleaning
    - Handling missing values
    - Removing duplicates
    - Normalizing
    - Encoding categorically
```python
df.ffill(inplace = True)
# df.fillna(method = 'ffill', inplace = True) is now deprecated
```
```python
df.drop_duplicates(inplace = True)
```
```python
scaler = MinMaxScaler()
numerical_cols = df.select_dtypes(include = ['number']).columns
df[numerical_cols] = scaler.fit_transform(df[numerical_cols])
```
```python
df = pd.get_dummies(df, drop_first = True)
```
<br>7. Store the cleaned data
```python
print('Cleaned Data:')
df.head()
``` 
```python
df.to_csv('cleaned_Heart.csv', index = False)
```
