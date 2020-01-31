---
title: "Linear Regression using Least-Square Method"
date: 2019-12-21
tags: [LR-LSM, R^2 Method, Standard Error, Data Science]
header:
  image: "/images/linear-regression-home.jpg"
excerpt: "LR-LSM, R^2 Method, Standard Error"
mathjax: "true"
---
## Simple Linear Regression 
In statistics, linear regression is a linear approach to modelling the relationship between a dependent variable and one or more independent variables. In the case of one independent variable it is called simple linear regression. For more than one independent variable, the process is called mulitple linear regression. We will be dealing with simple linear regression in this tutorial.
Let X be the independent variable and Y be the dependent variable.
    
                             Y = mX + c
             
### Whole Process  
![LRLSQM](/images/linear-regression-using-least-square-method.png)
[How to calculate linear regression using least square method
](https://youtu.be/JvS2triCgOY?list=PLF596A4043DBEAE9C)  

### Method  
![LRM](/images/linear-regression-method.png)  
[linear-regression-using-least-squares](https://towardsdatascience.com/linear-regression-using-least-squares-a4c3456e8570)  




```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
plt.rcParams['figure.figsize'] = (12.0, 10.0)
```


```python
# preprocessing input data
data = pd.read_csv('/dataset/data.csv')

x = data.iloc[:, 0]
y = data.iloc[:, 1]

plt.scatter(x, y)
plt.show()
```


![png](/images/output_4_0.png)



```python
# Building the model
x_mean = np.mean(x)
y_mean = np.mean(y)

num = 0
den = 0

for i in range(len(x)):
    num += (x[i] - x_mean) * (y[i] - y_mean)
    den += (x[i] - x_mean) ** 2

print(num, den, end="\n\n")

# calculate 'm'
m = num / den

# calculate 'c'
c = y_mean - m * x_mean

print(m, c)
```

    11754.427437779877 9130.66387904399
    
    1.287357370010931 9.908606190326509



```python
y_pred = m*x + c

plt.scatter(x, y)
# plt.scatter(x, y_pred)
plt.plot(x, y_pred, color="red")
plt.show()
```


![png](/images/output_6_0.png)


## Calculate R^2 Using Regression Analysis

### Visualization Process
![R Squared1](/images/r-square-method1.png)

### Calculation Process
![R Squared1](/images/r-square-method2.png)


```python
# calculate y - bar(y) ** 2
# calculate y_pred - bar(y) ** 2

actual = 0
prediction = 0

for i in range(len(y)):
    actual += (y[i] - y_mean) ** 2
    prediction += (y_pred[i] - y_mean) ** 2

print(actual, prediction)
```

    25771.72205622603 15132.148792284632



```python
r_square = prediction / actual
print(r_square)
```

    0.5871609494806324


## Standard Error of the Estimate used in Regression Analysis 
[standard-error](https://blog.minitab.com/blog/adventures-in-statistics-2/regression-analysis-how-to-interpret-s-the-standard-error-of-the-regression)

### Calculation process for SE in Regression Analysis
![se1](/images/standard-error1.png)

### SE Vs R^2
![se2](/images/standard-error2.png)


```python
# Calculate SE
est = 0

for i in range(len(y)):
    est += (y_pred[i] - y[i]) ** 2

n = len(y)
n = n - 2

SE = np.sqrt(est / n)

print(SE)
```

    10.473123808524093

