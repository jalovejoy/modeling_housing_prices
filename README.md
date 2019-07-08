# Advanced Linear Regression Price Modeling & Optimization with  Ames, IA Housing Data
<img src="https://raw.githubusercontent.com/jalovejoy/modeling_housing_prices/master/images/ames-aerial-view.JPG"
     alt="Markdown Monster icon"
     style="float: left; margin-right: 10px;" />

## Background Information
Ames, IA is a city with a population of around 66,000 ([US Census Bureau](https://www.census.gov/quickfacts/fact/table/amescityiowa/PST045217)) and is located 30 miles north of Des Moines. The housing data available for Ames is robust, making it an excellent market to practice housing price modeling, model optimization, and general data science techniques.

## Project Goal
The goal of this project was to construct a model that would effectively predict the price of a house based on key features. In the real world, the ideal model may take fewer features so that data collection is less time intensive. However, the model in this project was optimized for the Kaggle competition. Although it is currently feature heavy, clear instructions provide simple ways of paring down the model for more practical applications.

> "All models are wrong, but some are useful" - George Edward Pelham Box

## Project Outline

1. Importing Libraries & Loading Data
2. Cleaning & Preparing Data
    1. Renaming columns
    2. Dropping bad data
    3. Resetting values & types
3. Populating Null Values
4. Adding Metrics
5. Exploratory Data Analysis
    1. General EDA
    2. Feature EDA
6. EDA & Model for Null BsmtQual
7. Model Testing
    1. Setting models
    2. Testing models
    3. Grid search optimization
    4. Visualizing model
8. Running Model on Test Data

## Data Dictionary

This represents the data used in the model and/or model construction. The initial dataset can be found [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt) and contains 81 features. Below represents the engineered features included in this model.


|Feature|Type|Description|Included in Model|
|---|---|---|---|
|HouseAge|int|How old the house is since year built| Not in model|
|TotalArea|float|Composite metric of weighted Basement, Ground Floor, and Garage Area minus Low Quality Basement Area|Included|
|QualMetric|float|Composite score of weighted Overall, Kitchen, Basement, and External Quality scores|Included|
|TotalBaths|float|Sum of full baths and half baths (counted as a half)|Included|
|PorchArea|int|Sum of areas for Screen Porch, 3 Season Porch, Open Porch, Enclose Porch, and Wood Deck|Included|
|Neighborhood_Edwards|uint|Dummy variable indicates whether house is in Edwards|Included|
|Neighborhood_IDOTRR|uint|Dummy variable indicates whether house is in Iowa DOT and Rail Road|Included|
|Neighborhood_NAmes|uint|Dummy variable indicates whether house is in Northwest Ames|Included|
|Neighborhood_NoRidge|uint|Dummy variable indicates whether house is in Northridge|Included|
|Neighborhood_NridgHt|uint|Dummy variable indicates whether house is in Northridge Heights|Included|
|Neighborhood_OldTown|uint|Dummy variable indicates whether house is in Old Town|Included|
|Neighborhood_Somerst|uint|Dummy variable indicates whether house is in Somerset|Included|
|Neighborhood_StoneBr|uint|Dummy variable indicates whether house is in Stone Brook|Included|
|MSSubClass_30|uint|Dummy variable indicates whether house is 1-STORY 1945 & OLDER|Not in model|
|MSSubClass_50|uint|Dummy variable indicates whether house is 1-1/2 STORY FINISHED ALL AGES|Not in model|
|MSSubClass_60|uint|Dummy variable indicates whether house is 2-STORY 1946 & NEWER|Not in model|
|mansion|int|Dummy variable indicates whether house is a mansions (TotalArea > 5000 SF)|Included|



## Executive Summary

**Data Cleaning:** While the Ames dataset was robust it was also quite messy. There were 81 columns in the training data. In both the training and test data there were many columns with Null values. The first step I took was to drop the columns with more than 30% missing data. Simply put, these wouldn't be useful to making predictions. I then used the MissingNo library to examine the remaining columns with Null values. However, before dropping, cleaning, or filling these columns, I did some exploration of the data to see if there would be any correlations and determine what columns would be worth salvaging. In the end, I decided that cleaning columns that showed no sign of having valuable signals for my target, the Sale Price, would be a waste of time.

**Data Creation & Preparation:** I engineered a few key columns of data to support my model. First, one critical element for my model was resetting all of the quality metrics as numeric values (ie. Ex or Extremely Good to 5 and Po or Poor to 1). Next, I took combined scores that I noticed represented similar attributes. Specifically, I combined all of the Quality metrics into one score, all of the Square Footage or Area metrics into one score, the total of Baths as one score, and the total Porches or Decks into one score. With this view I was able to get simple scores that each provided a holistic view of distinct elements. Addditionally, I built a function that identified the Neighborhoods that had the strongest (>0.15) effect on Sale Price. The test data was missing some values in the Basement Quality field – I engineered a model to predict what these would be based on other features in the test data and used that to fill in the Nulls. Finally, after identifying two "mansions" in the EDA and model review, I added a mansions variable based for buildings with >5,000 Total Area.

**Exploratory Data Analysis:** The EDA I conducted was relatively straightforward but it allowed me to bypass cleaning _every_ variable in the dataset and focus on the ones that mattered in my model. I initially used the basic .head(), .info(), and the MissingNo matrix to get familiar with the data. Recognizing that Sale Price may not be linear (ie. lots of low- or mid-priced houses but only a few high-end houses), I created histograms for both Sale Price and the log of Sale Price – indeed, the log of Sale Price allowed me to work with a normal distribution. The core of my EDA centered around visualizing correlations in the heatmap. I took a ludicrously large heatmap so that I could examine _every_ variable's correlation on Sale Price. Again, doing the EDA early and keeping the scope extremely wide, I was able to quickly hone in on variables that would indicate Sale Price. Finally, I plotted the variables I found useful on scatter plots and heatmaps so I could better understand their relationship with Sale Price and one another. There was some indication of colinearity between certain variables (Quality & Total Area, Quality & Year Remodeled) but not enough for me to be concerned about the integrity of the model.

**Model Testing & Optimization:** The features I selected were then put through a rigorous model selection process that evaluated Cross Validation scores (5 K-Folds) across Linear Regressions, Lasso Regressions, Ridge Regressions, and Elastic Regressions both using a Standard Scaler and Power Transformation. After testing the performance of each, using the Power Transformation on the features and inputting them into a Ridge model delivered the best Cross Validation scores. I then fit the model and created predictions and error scores. To better understand the model performance, I created a scatter plot (Actuals vs Predictions), a histogram of errors (to ensure errors were normal), and a kernel density plot. Finally, I took the 5 most over and under predicted houses and examined the features that they collectively over- and under-indexed on to identify if there were other features worth incorporating to mitigate the strongest outliers.

**Running the Model:** In 8 lines of code I fit the model, created my predictions, and exported them as a CSV to submit to the Kaggle competition.