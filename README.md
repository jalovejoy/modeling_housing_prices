# Project 2: Advanced Linear Regression Price Modeling & Optimization with  Ames, IA Housing Data
<img src="../images/ames-aerial-view.jpg"
     alt="Markdown Monster icon"
     style="float: center; margin-right: 10px;" />

## Background Information
Ames, IA is a city with a population of around 66,000 ([US Census Bureau](https://www.census.gov/quickfacts/fact/table/amescityiowa/PST045217)) and is located 30 miles north of Des Moines. The housing data available for Ames is robust, making it an excellent market to practice housing price modeling, model optimization, and general data science techniques.

## Project Goal
The goal of this project was to construct a model that would effectively predict the price of a house based on key features. In the real world, the ideal model may take fewer features so that data collection is less time intensive. However, the model in this project was optimized for the Kaggle competition. Although it is currently feature heavy, clear instructions provide simple ways of paring down the model for more practical applications.

> "All models are wrong, but some are useful" - George Edward Pelham Box

## Project Outline

1. Importing Libraries & Loading Data
2. Cleaning & Preparing Data
    1. Renaming columns
    2. Dropping bad data](#DropBadData)
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
|---|---|---|
|HouseAge|int|How old the house is since year built| Not in model|
| TotalArea|float|Composite metric of weighted Basement, Ground Floor, and Garage Area minus Low Quality Basement Area|Included|
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


## Repository Structure

## Executive Summary
