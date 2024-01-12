# House-Sales-in-King-County-USA


# Objectives:
- Load the data as a pandas dataframe
- Clean the data, taking care of the blank entries
- Run exploratory data analysis and identify the attributes that most affect the charges
- Develop single variable and multi variable Linear Regression models for predicting the charges
- Use Ridge regression to refine the performance of Linear regression models.


# libraries:
- import pandas as pd
- import matplotlib.pyplot as plt
- import numpy as np
- import seaborn as sns
- from sklearn.pipeline import Pipeline
- from sklearn.preprocessing import StandardScaler,PolynomialFeatures
- from sklearn.linear_model import LinearRegression
%matplotlib inline


## Importing Data Sets
```
file_name='https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/coursera/project/kc_house_data_NaN.csv
df=pd.read_csv(file_name)
```

## We use the method head to display the first 5 columns of the dataframe.
```
df.head()
df
```
## Display the data types of each column using the attribute dtype, then take a screenshot and submit it, include your code in the image.
```
df.dtypes
```
## We use the method describe to obtain a statistical summary of the dataframe.
```
df.describe()
```

## Drop the columns "id" and "Unnamed: 0" from axis 1 using the method drop(), then use the method describe() to obtain a statistical summary of the data. Take a screenshot and submit it, make sure the inplace parameter is set to True
```
df.drop('id',"Unnamed: 0", axis = 1, inplace = True)
df.describe()
```
## We can see we have missing values for the columns  bedrooms and  bathrooms 
```
print("number of NaN values for the column bedrooms :", df['bedrooms'].isnull().sum())

print("number of NaN values for the column bathrooms :", df['bathrooms'].isnull().sum())
```

## We can replace the missing values of the column 'bedrooms' with the mean of the column 'bedrooms'  using the method replace(). Don't forget to set the inplace parameter to True
```
mean=df['bedrooms'].mean()
df['bedrooms'].replace(np.nan,mean, inplace=True)
```

## We also replace the missing values of the column 'bathrooms' with the mean of the column 'bathrooms'  using the method replace(). Don't forget to set the  inplace  parameter top  True 
```
mean=df['bathrooms'].mean()
df['bathrooms'].replace(np.nan,mean, inplace=True)

print("number of NaN values for the column bedrooms :", df['bedrooms'].isnull().sum())

print("number of NaN values for the column bathrooms :", df['bathrooms'].isnull().sum())
```

## Use the method value_counts to count the number of houses with unique floor values, use the method .to_frame() to convert it to a dataframe.
```
y = df['floors'].value_counts().to_frame()
y
```
## Use the function boxplot in the seaborn library to determine whether houses with a waterfront view or without a waterfront view have more price outliers.
```
sns.boxplot(x = 'waterfront',  y = 'price', data = df)
```
## Use the function regplot in the seaborn library to determine if the feature sqft_above is negatively or positively correlated with price. 
```
sns.regplot(x = 'sqft_above', y = 'price', data = df)
```







