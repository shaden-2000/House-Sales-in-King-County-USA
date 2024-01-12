# House-Sales-in-King-County-USA

In this project, i will have to perform analytics operations on an insurance database that uses the below mentioned parameters.


<img width="546" alt="Screenshot 1445-06-30 at 10 03 51 PM" src="https://github.com/shaden-2000/House-Sales-in-King-County-USA/assets/100734021/4ad83ffc-d187-4805-bdb0-85771e64c343">



# Objectives:
- Load the data as a pandas dataframe
- Clean the data, taking care of the blank entries
- Run exploratory data analysis and identify the attributes that most affect the charges
- Develop single variable and multi variable Linear Regression models for predicting the charges
- Use Ridge regression to refine the performance of Linear regression models.

# Setup

### For this lab, we will be using JupyterLite
### For this lab, we will be using the following libraries:

- skillsnetwork to download the data
- pandas for managing the data.
- numpy for mathematical operations.
- sklearn for machine learning and machine-learning-pipeline related functions.
- seaborn for visualizing the data.
- matplotlib for additional plotting tools.


## importing Required Libraries¶
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler, PolynomialFeatures
from sklearn.linear_model import LinearRegression, Ridge
from sklearn.metrics import mean_squared_error, r2_score
from sklearn.model_selection import cross_val_score, train_test_split

```



## Download the dataset

1- load the dataset to this environment if you using JupyterLite,which requires the dataset to be downloaded to the interface. 
```
from pyodide.http import pyfetch

async def download(url, filename):
    response = await pyfetch(url)
    if response.status == 200:
        with open(filename, "wb") as f:
            f.write(await response.bytes())

```

2- if you using Jupyter Anaconda, which working in local machines,simply use the URL directly in the pandas.read_csv() function. 
```
#filepath = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DA0101EN-Coursera/medical_insurance_dataset.csv'
#df = pd.read_csv(filepath, header=None)
```


## Import the dataset
Import the dataset into a pandas dataframe. Note that there are currently no headers in the CSV file.

Print the first 10 rows of the dataframe to confirm successful loading.
```
df = pd.read_csv(file_name, header=None)
print(df.head(10))
```
## Add the headers to the dataframe
```
headers = ["age", "gender", "bmi", "no_of_children", "smoker", "region", "charges"]
df.columns = headers
```

## replace the '?' entries with 'NaN' values.
```
df.replace('?', np.nan, inplace = True)
```

## Use dataframe.info() to identify the columns that have some 'Null' (or NaN) information.
```
print(df.info())
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







