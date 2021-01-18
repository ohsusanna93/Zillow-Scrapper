# Zillow Real Estate Pricing (San Diego, CA)

# Introduction

A Zillow Scrapper was created to analyze all properties listed on Zillow, a real estate website used to sell, buy, and rent. The Zillow Scrapper is able to bring great insight to the different features that are compared and displayed with any available property listed on the website. Many future homebuyers, renters, and potential clients use Zillow in search of their new home. It is also a common tool used by real estate agents/companies to list their properties. 

A linear regression model as well as the Random Forest method will be used to compare the relationship between the features and the price. The columns in our data frame and listed below.

    - price of property
    - type of property
    - postalcode
    - city
    - url to listing
    - floorsize in sqft
    - number of bedrooms
    - number of bathrooms
    - agent/company selling the property
    - location: suburb or city

The city and suburbs scrapped in this project are:
    - San Diego and La Jolla (city)
    - Chula Vista, La Mesa, El Cajon, Carlsbad, Escondido, Oceanside, Encinitas, Cardiff, San Marcos, 
      Solana Beach', Del Mar, Coronado, Poway, Santee, Vista, and Spring Valley.
      
The definition of the type of homes are listed below: 
    - House
    - Condo
    - Townhouse 
    - Multi-Family (apartments)
    - Pre-foreclosure (30-120 grace period for current tenents to pay overdue balance)
    - Foreclosure (owners selling the mortgaged property to recover the amount owed)
    - Auction (owned by bank or agent)

The two methods used are OLS and Random Forest using RandomizedSearchCV. Ordinary Least Squares is a method that estimates the relationship between every variable with the independent variable. It minimizes the sum of the squares between the observed and predicited values often shown as a linear line.RandomizedSearchCV is an algorithm used to find the best combination of parameters in the model to increase teh accuracy of the random forest method in making predictions.

## Libraries: 


import requests
import json
import csv
from bs4 import BeautifulSoup
import time
import statsmodels.api as sm
from statsmodels.formula.api import ols
import statsmodels.stats.api as sms
import statsmodels.formula.api as smf
plt.style.use('seaborn')
import scipy.stats as stats
%conda update scikit-learn
!pip install imblearn
from sklearn.model_selection import train_test_split, RandomizedSearchCV
from sklearn.ensemble import RandomForestClassifier
from sklearn import metrics
from sklearn.metrics import accuracy_score
 
from imblearn import under_sampling, over_sampling
from imblearn.over_sampling import SMOTE
import warnings
warnings.filterwarnings('ignore')



# Pre-Process Data


We creataed another column named 'location' to split the cities into two categories: suburbs and city and printed all the unique values in each column to see what our dataset looks like. Then cleaned out all symbols and signed and getting rid of any null values.



# Explore Data


Check the histograms of the columns to get a general idea of the data distribution within the categories. If it looks like a bar graph it is another indication that it is a categorical data. If it is a even hill in the middle the data is distributed normally.


We can check each column using the function check_columns this allows us to quickly view the relationship between the column and the independent variable, price. It is a fast way to check for outliers and distribution too.


Matrix Graph. Comparing every column with the percentage of correlation displayed. The correlation is then color coded with an orange color gradient displaying darker shades with larger percentages. This way we are able to spot high correlated/overlapping columns efficiently. As we can see floorsize and bathrooms have the highest percentage of 88% but due to the understanding of the two columns we have decided to keep both columns for our model.



The find_outliers function helps indicate the outiers within the specified column and drops the necessary rows which contain variables outside the temporary z-score guidelines (>3 and <-3). The find_outliers function was not used if the called column did not improve the model.




# Linear Regression and Random Forest Model

Two types of models were used to analyze the data extracted. 

Ordinary Least Squares is a method that estimates the relationship between every variable with the independent variable. It minimizes the sum of the squares between the observed and predicted values often shown as a linear line.


Random Forest is an algorithm that consist of many decision trees using random subsets of features that averages the outcome to make predictions.

RandomizedSearchCV is an algorithm that takes the input of parameters and attempts every combination and outputs the best hyper parameters for the model.




# RESULTS and CONCLUSION

The r squared value in our linear regression model increased as we took away the location and seller variables, resulting in a r squared value of 0.799. Which can be interpretted as a 80% correlation. 

The random forest model performed well with the top three correlated features being floorsize, postalcode, and city. The model was able to predict the price point of a property based on the features 99% accurately. 

When comparing the two models the Random forest was able to provide more in depth and accurate information in what the market looks like in San Diego. Although there were not many independent variables to come to a groundbreaking insight in the real estate market. The potential of these models are exciting to see as we continue to collect more data about the properties being listed. For future work we will be scraping more facts and features of each property to even further more discover the different variables affecting the market.


# INSIGHTS and RECOMMENDATIONS

1. It is important to know that the floorsize and location of the property will have the biggest impact on the price of the home. We are also interested in calculating the price/sqft to compare the low, average, and high cost properties.

2. For homebuyers: The agent(s) or company showing the property has an impact on the the price range of the homes because they only try to sell certain types of homes at a certain price point.

3. The specific postalcode area will have more affect on the price of the property than if the property is located in the city or suburb.

# Future Work 

I will continue to extract more data that is available on Zillow to add more features to compare and analyze the properties to bring more insight to the real estate market.