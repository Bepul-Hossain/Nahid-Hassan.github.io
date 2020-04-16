---
title: "Introduction to pandas part-1"
date: 20120-04-16
tags: [Pandas, DataFrame]
header:
  # image: "/images/logistic-regression-titanic-data-analysis/Runner.png"
excerpt: "Pandas"
mathjax: "true"
---
# Extracting and transforming data


```python
import pandas as pd
from glob import glob
```


```python
data_files = glob('./datasets/*')
sales_data_files = glob('./datasets/sales/*')
```


```python
data_files
```




    ['./datasets/all_medalists.csv',
     './datasets/gapminder_tidy.csv',
     './datasets/pennsylvania2012_turnout.csv',
     './datasets/pittsburgh2013.csv',
     './datasets/sales',
     './datasets/sales.zip',
     './datasets/titanic.csv',
     './datasets/users.csv']




```python
sales_data_files
```




    ['./datasets/sales/sales-feb-2015.csv', './datasets/sales/sales.csv']




```python
sales = pd.read_csv(sales_data_files[1], index_col='month')
```


```python
sales.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Indexing using square brackets
sales['salt']['Jan'] # sales[col_index_name][row_index_name] 
```




    12.0




```python
# Using column a!ribute and row label
sales.eggs['Mar'] # salse.eggs select eggs column and then using ['Mar']  to select specific attribute
```




    221




```python
# Using the .loc accessor
sales.loc['Apr', 'spam'] # DataFrame.loc['row_index_name', 'col_index_name']
```




    20




```python
# Using the .iloc accessor
sales.iloc[1, 2] # DataFrame.iloc[row_index, col_index] 
# To select Feb, spam attribute
```




    31




```python
# Selecting only some columns
sales[['spam', 'eggs']] # [pass_a_list_of_column_names]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>spam</th>
      <th>eggs</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>17</td>
      <td>47</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>31</td>
      <td>110</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>72</td>
      <td>221</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>20</td>
      <td>77</td>
    </tr>
    <tr>
      <th>May</th>
      <td>52</td>
      <td>132</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>55</td>
      <td>205</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Slicing DataFrames
```


```python
# Selecting a column (i.e., Series)
sales['eggs']
```




    month
    Jan     47
    Feb    110
    Mar    221
    Apr     77
    May    132
    Jun    205
    Name: eggs, dtype: int64




```python
type(sales['eggs'])
```




    pandas.core.series.Series




```python
# Slicing and indexing a Series
sales['eggs'][2:4] # select 3rd and 4rth rows from eggs columns
```




    month
    Mar    221
    Apr     77
    Name: eggs, dtype: int64




```python
sales['eggs'][4] # select only 4rth rows from eggs columns
```




    132




```python
sales['eggs'][::2] # select 0th, 2nd, 4th........... rows from eggs columns
```




    month
    Jan     47
    Mar    221
    May    132
    Name: eggs, dtype: int64




```python
# Using .loc[] (1)
sales.loc[:, 'eggs':'salt'] # All rows, some columns
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using .loc[] (2)
sales.loc['Jan' : 'Apr', :] # some rows, all columns
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using .loc[] (3)
sales.loc['Mar':'May', 'salt':'spam'] # some rows, some columns
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mar</th>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>NaN</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using .iloc[]
sales.iloc[2:5, 1:] # A block from middle of the DataFrame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mar</th>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>NaN</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using lists rather than slices (1)
sales.loc['Jan':'May', ['eggs', 'spam']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using lists rather than slices (2)
sales.iloc[[0,4,5], 0:2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Series versus 1-column DataFrame
sales['eggs'], type(sales['eggs'])
```




    (month
     Jan     47
     Feb    110
     Mar    221
     Apr     77
     May    132
     Jun    205
     Name: eggs, dtype: int64,
     pandas.core.series.Series)




```python
# Series versus 1-column DataFrame
sales[['eggs']], type(sales[['eggs']])
```




    (       eggs
     month      
     Jan      47
     Feb     110
     Mar     221
     Apr      77
     May     132
     Jun     205,
     pandas.core.frame.DataFrame)




```python
# Filtering  DataFrames
```


```python
# Creating a Boolean Series
sales.salt > 60
```




    month
    Jan    False
    Feb    False
    Mar     True
    Apr     True
    May    False
    Jun    False
    Name: salt, dtype: bool




```python
# Filtering with a Boolean Series
sales[sales.salt > 60]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
enough_salt_sold = sales.salt > 60
```


```python
sales[enough_salt_sold]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Combining filters
sales[(sales.salt >= 50) & (sales.eggs < 200)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales[(sales.salt >= 50) | (sales.eggs < 200)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# DataFrames with zeros and NaNs
demo = sales.copy()
```


```python
demo
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
demo['bacon'] = [0,0,23,56,44,0]
```


```python
demo
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>bacon</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
      <td>23</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
      <td>56</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>44</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select columns with all nonzeros
demo.loc[:, demo.all()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select columns with any nonzeros
demo.loc[:, demo.any()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>bacon</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
      <td>23</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
      <td>56</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>44</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select columns with any NaNs
sales.loc[:, sales.isnull().any()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>salt</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>12.0</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>50.0</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>89.0</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>87.0</td>
    </tr>
    <tr>
      <th>May</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Select columns without NaNs
sales.loc[:, sales.notnull().all()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop rows with any NaNs
sales.dropna(how='any')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>221</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>77</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>205</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Filtering a column based on another
sales.eggs[sales.salt > 55]
```




    month
    Mar    221
    Apr     77
    Jun    205
    Name: eggs, dtype: int64




```python
# Modifying a column based on another
sales.eggs[sales.salt > 55] += 5
```


```python
sales
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Transforming DataFrames
```


```python
# DataFrame vectorized methods
sales.floordiv(12)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>3</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>9</td>
      <td>4.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>18</td>
      <td>7.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>6</td>
      <td>7.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>May</th>
      <td>11</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>17</td>
      <td>5.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales # no change in original DataFrame
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
    </tr>
  </tbody>
</table>
</div>




```python
# NumPy vectorized functions

import numpy as np 

np.floor_divide(sales, 12)  # Convert to dozens unit
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>3.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>9.0</td>
      <td>4.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>18.0</td>
      <td>7.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>6.0</td>
      <td>7.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>May</th>
      <td>11.0</td>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>17.0</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plain Python functions (1)

def dozens(n):
    return n // 12

sales.apply(dozens)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>3</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>9</td>
      <td>4.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>18</td>
      <td>7.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>6</td>
      <td>7.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>May</th>
      <td>11</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>17</td>
      <td>5.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plain Python functions (2)
sales.apply(lambda n : n // 12)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>3</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>9</td>
      <td>4.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>18</td>
      <td>7.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>6</td>
      <td>7.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>May</th>
      <td>11</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>17</td>
      <td>5.0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Storing a transformation
sales['dozen_of_eggs'] = sales.eggs.floordiv(12)
```


```python
sales
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>dozen_of_eggs</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
      <td>6</td>
    </tr>
    <tr>
      <th>May</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>11</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
# The DataFrame index
sales.index
```




    Index(['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'], dtype='object', name='month')




```python
# Working with string values (1)
sales.index = sales.index.str.upper()
```


```python
sales.index
```




    Index(['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN'], dtype='object', name='month')




```python
sales
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>dozen_of_eggs</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>JAN</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>3</td>
    </tr>
    <tr>
      <th>FEB</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>9</td>
    </tr>
    <tr>
      <th>MAR</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
      <td>18</td>
    </tr>
    <tr>
      <th>APR</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
      <td>6</td>
    </tr>
    <tr>
      <th>MAY</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>11</td>
    </tr>
    <tr>
      <th>JUN</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Working with string values (2)
sales.index = sales.index.map(str.lower)
```


```python
sales
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>dozen_of_eggs</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>3</td>
    </tr>
    <tr>
      <th>feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>9</td>
    </tr>
    <tr>
      <th>mar</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
      <td>18</td>
    </tr>
    <tr>
      <th>apr</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
      <td>6</td>
    </tr>
    <tr>
      <th>may</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>11</td>
    </tr>
    <tr>
      <th>jun</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
      <td>17</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Defining columns using other columns
sales['salty_eggs'] = sales.eggs + sales.dozen_of_eggs
```


```python
sales
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eggs</th>
      <th>salt</th>
      <th>spam</th>
      <th>dozen_of_eggs</th>
      <th>salty_eggs</th>
    </tr>
    <tr>
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>jan</th>
      <td>47</td>
      <td>12.0</td>
      <td>17</td>
      <td>3</td>
      <td>50</td>
    </tr>
    <tr>
      <th>feb</th>
      <td>110</td>
      <td>50.0</td>
      <td>31</td>
      <td>9</td>
      <td>119</td>
    </tr>
    <tr>
      <th>mar</th>
      <td>226</td>
      <td>89.0</td>
      <td>72</td>
      <td>18</td>
      <td>244</td>
    </tr>
    <tr>
      <th>apr</th>
      <td>82</td>
      <td>87.0</td>
      <td>20</td>
      <td>6</td>
      <td>88</td>
    </tr>
    <tr>
      <th>may</th>
      <td>132</td>
      <td>NaN</td>
      <td>52</td>
      <td>11</td>
      <td>143</td>
    </tr>
    <tr>
      <th>jun</th>
      <td>210</td>
      <td>60.0</td>
      <td>55</td>
      <td>17</td>
      <td>227</td>
    </tr>
  </tbody>
</table>
</div>


