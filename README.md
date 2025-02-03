# sales_Analysis-
The Sales Analysis project is designed to analyze sales data from various products, focusing on user ratings, timestamps, and product attributes. 

# The dataset gives us electronics sales data at Amazon. 

# It contains user ratings for various electronics items sold, along with category of each item and time of sell.

# The dataset is available at https://www.kaggle.com/datasets/edusanketdk/electronics

# Importing the libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# visualization

import seaborn as sns

# Importing the dataset

dataset = pd.read_csv("C:/Users/dell/Downloads/Amazon_Electronics_Products_Sales/electronics.csv")

# list of first five rows

dataset.head(5)

dataset.tail()

dataset.shape

dataset.info()

# We can also see that there are no null values in the dataset.

# We can also see that the column Timestamp is of int64 data type, but it is actually a timestamp.

# We can convert it to a timestamp using the following code:

from datetime import datetime

pd.to_datetime(dataset['timestamp'])

# We can also see that the column Product ID is of object data type, but it is actually a string.

# We can convert it to a string using the following code:

dataset['brand'] = dataset['brand'].astype(str)
dataset['category']=dataset['category'].astype(str)


# We can convert it to a timestamp using the following code:
dataset['timestamp'] = pd.to_datetime(dataset['timestamp'])



# We can convert it to a float using the following code:
dataset['rating'] = dataset['rating'].astype(float)

dataset['user_id'] = dataset['user_id'].astype(str)
dataset['item_id'] = dataset['item_id'].astype(str)

dataset.describe()


# the statistical summary of the dataset gives us the following information:

# 1. The mean rating is 4.

# 2. The minimum rating is 1.

# 3. The maximum rating is 5.

# 4. The standard deviation of the ratings is 1.4.

# 5. The 25th percentile of the ratings is 4.

# 6. The 50th percentile of the ratings is 5.

# 7. The 75th percentile of the ratings is 5.

#the number of unique users and items in the dataset
dataset.nunique()

#checking for duplicates
dataset.duplicated().sum()

#checking for missing values
dataset.isnull().sum()

#the distribution of ratings
dataset['rating'].value_counts()

#most of the ratings are 5 


# what was the best year of sales

dataset['year'] = pd.DatetimeIndex(dataset['timestamp']).year

dataset['year'].value_counts()

#according to the analysis 2015 was the best year of sales 

# what was the best month of sales
dataset['month']=pd.DatetimeIndex(dataset['timestamp']).month
dataset['month'].value_counts()

# January was the best month of sales

# drop all null values

dataset.dropna(inplace=True)

# check for missing values

dataset.isnull().sum()

dataset.nunique()

# Finding Answers with DATA WE HAVE with visualizations 


#the distribution of ratings 
sns.countplot(x='rating',data=dataset)

# the distribution of ratings

# The distribution of ratings is as follows:

# most of the ratings are 5

dataset['rating'].value_counts()

#distribution of sales by year 
sns.countplot(x='year',data=dataset)

#setting global figure size 
sns.set(rc={'figure.figsize':(14,10)})

#according to the visualization 
#2015 was the best year for sale 


#brands with the most sales 
sns.countplot(x='brand',data=dataset,order=dataset['brand'].value_counts().iloc[1:10].index)

## Logitech & Bose had the most sales followed by Sony.

sns.countplot(x='brand',data=dataset,order=dataset['brand'].value_counts().iloc[-10:].index)

#according to this graph , EINCAR has the least sale 

#brands with the most sales in 2016 
sns.countplot(x='brand',data=dataset[dataset['year']==2016],order=dataset['brand'].value_counts().iloc[1:10].index)
sns.set(rc={'figure.figsize':(14,12)})

# in 2016 Bose overtook Logitech to have the most sales.

#the top 3 products sold in 2016 were Bose , Logitech & TooTronics 

#brand with the most sales in 2017 
sns.countplot(x='brand',data=dataset[dataset['year']==2017],order=dataset['brand'].value_counts().iloc[1:6].index)

#Bose has the most sales in 2017
#top 3 Bose>Logitech>Mpow

# brands with the most sales in 2018

sns.countplot(x='brand', data=dataset[dataset['year'] == 2018], order=dataset['brand'].value_counts().iloc[1:6].index)


# For 2018, Bose was the most sold for a third year in a row followed by Logitech while Mpow was the third most sold.


#month the most sale 
sns.countplot(x='month',data=dataset)

#January [#1] was the month with the most 

# What products by category were sold the most in January
sns.countplot(x='category',data=dataset[dataset['month']==1],order=dataset['category'].value_counts().iloc[1:10].index)

#computers & Accessories has most sale

# Category with the least sales

sns.countplot(x='category', data=dataset, order=dataset['category'].value_counts().iloc[-6:].index)


#security &Surveillance has least sale 

#How much was made in sales in the year 2015
dataset[dataset['year']==2015].groupby('year')['rating'].count().plot(kind='bar')

#best month 
dataset['month']=pd.DatetimeIndex(dataset['timestamp']).month
dataset.groupby('month')['rating'].count().plot(kind='bar')

#from this graph,we can clearly see that , January had the best for sales .

#what product by category sold the most ?
dataset.groupby('category')['rating'].count().sort_values(ascending=False).head(10).plot(kind='bar')

#from the above graph , we can see that , Headphones sold the most 

# brand percentage sales

dataset.groupby('brand')['rating'].count().sort_values(ascending=False).head(8).plot(kind='pie')
sns.set(rc={'figure.figsize':(4,8)})

#according to the analysis ,the brand name of NaN had the most sales 

#distribution of sales presented in a pie chart 
dataset['category'].value_counts(normalize=True)
dataset.groupby('category')['rating'].count().sort_values(ascending=False).head(10).plot(kind='pie')

#background colour 
sns.set_style('dark')

# conclusion of our analysis

# We can see that the year 2015 had the best sales.

# The month of January had the best sales.

# We can see that the brands Bose and Logitech sold the most

# We can see that the category of Headphones sold the most.

#NaN brand had the most sales 

# We can see that the brand name of EINCAR sold the least followed closely with DURAGADGET.

# We can see that the category of Security and Surveillance sold the least.




