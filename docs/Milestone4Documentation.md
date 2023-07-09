# CS-634-Data-Mining

<p align="center">
<img src="/docs/img/njitlogo.png">
</p>

<p align="center">
NJIT Summer 2023 <br> CS 634 Data Mining <br> Interpretable Gradient Boosting - Real Estate House Price Prediction Project <br> By: Chiara Vega
</p>

---

# Project Links

- [Kaggle Housing Prices Prediction Dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)
- [Demo](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-4/README.md)
- [App Landing Page](https://sites.google.com/njit.edu/real-estate-housing/)
- [HF Streamlit App](https://huggingface.co/spaces/HFcpv24/LightGBM-House-Sale-Price-Prediction)
- [Notebook](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-4/CS634_CVega_Notebook.ipynb)

---

# Table of Contents
1. [Abstract](#abstract)
2. [Introduction](#introduction)

   2.1 [Approach](#approach)
   
   2.2 [Dataset](#dataset)

3. [Getting Started](#getting-started)

   3.1 [Installation](#installation)

   3.2 [Import Libraries and Load Dataset](#import-libraries-and-load-dataset)

4. [Exploratory Data Analysis](#exploratory-data-analysis)

   4.1 [Target Variable: SalePrice Distribution](#target-variable-saleprice-distribution)

   4.2 [Descriptive Statistics](#descriptive-statistics)

   4.3 [Identifying Missing Values](#identifying-missing-values)

5. [Data Preprocessing](#data-preprocessing)

   5.1 [Skewed Distribution](#skewed-distribution)

   5.2 [Missing Values and Categorical Features](#missing-values-and-categorical-features)

6. [Split Training and Test Sets](#split-training-and-test-sets)

7. [Baseline](#baseline)

   7.1 [Baseline Model Training, Evaluation, and Predictions](#baseline-model-training-evaluation-and-predictions)
   
   7.2 [Baseline SHAP Summary and Interaction Plots](#baseline-shap-summary-and-interaction-plots)

8. [Hyperparameter Optimization via Optuna](#hyperparameter-optimization-via-optuna)

   8.1 [Tuned Model Training, Evaluation, and Predictions](#tuned-model-training-evaluation-and-predictions)

   8.2 [Tuned SHAP Summary and Interaction Plots](#tuned-shap-summary-and-interaction-plots)

9. [HuggingFace Streamlit App](#huggingface-streamlit-app)

   9.1 [App Results](#app-results)

10. [App Landing Page](#app-landing-page)
11. [Demo](#demo)
12. [Conclusion](#conclusion)
13. [References](#references)

# Abstract

<p align="justify">
Provided within this documentation are extensive accounts of my methodology, findings, and insightss. The Interpretable Gradient Boosting - Real Estate House Price Prediction Project leveraged machine learning techniques to develop a predictive model and interpretable framework that can accurately predict housing sales prices (target variable: <code>SalePrice</code> based on various Ames, Iowa housing features (79 to be exact) such as year built, area square footage, number of bedrooms, etc. In <code>milestone-1</code>, the task was to get familiar with <code>Docker</code>. The machine learning model and SHapley Additive exPlanations plots were built in <code>milestone-2</code>, whereas <code>milestone-3</code> built upon the previous milestone by performing hyperparamter optimization with Optuna and added the creating of the HuggingFace streamlit app. For the final milestone, <code>milestone-4</code>, the task was to finalize the project by means of extensive documentation, creating a Google Sites landing page for the streamlit app, and producing a demo video of the app.
</p>

# Introduction

## Approach
<p align="justify">
Due to the sheer variety and number of factors that affect house pricing, determining the sale price of a house if often challenging - a problem faced by realtors, homeowners, and buyers alike. Thus, the project aims to build a machine learning model that, based on the dataset, can predict the sale price of a house - being aware that machine learning can offer promising solutions to tackle the prediction challenge and task at hand. The models utilized in this project are LightGBM and XGBoost, whereas SHAP plots are used for interpretable (or explainable) machine learning. Optimization will be explored as well as the development of the HuggingFace streamlit app which provides an interface for users to experiment with the trained models. Prior to taking on these steps, however, are the Exploratory Data Analysis and data preprocessing steps, which will be discussed shortly.
</p>

## Dataset

The [Kaggle Housing Prices Prediction Dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview) featuring data on Ames, Iowa homes, originally prepared by Dean De Cock, comprises 4 files: 

>train.csv - the training set
>
>test.csv - the test set
>
>data_description.txt - full description of each column, originally prepared by Dean De Cock but lightly edited to match the column names used here
>
>sample_submission.csv - a benchmark submission from a linear regression on year and month of sale, lot square footage, and number of bedrooms

Contained within the dataset are 79 explanatory variables and a little over 2.9k observations. The 79 features are as follows:

>SalePrice - the property's sale price in dollars. This is the target variable that you're trying to predict.
>
>MSSubClass: The building class
>
>MSZoning: The general zoning classification
>
>LotFrontage: Linear feet of street connected to property
>
>LotArea: Lot size in square feet
>
>Street: Type of road access
>
>Alley: Type of alley access
>
>LotShape: General shape of property
>
>LandContour: Flatness of the property
>
>Utilities: Type of utilities available
>
>LotConfig: Lot configuration
>
>LandSlope: Slope of property
>
>Neighborhood: Physical locations within Ames city limits
>
>Condition1: Proximity to main road or railroad
>
>Condition2: Proximity to main road or railroad (if a second is present)
>
>BldgType: Type of dwelling
>
>HouseStyle: Style of dwelling
>
>OverallQual: Overall material and finish quality
>
>OverallCond: Overall condition rating
>
>YearBuilt: Original construction date
>
>YearRemodAdd: Remodel date
>
>RoofStyle: Type of roof
>
>RoofMatl: Roof material
>
>Exterior1st: Exterior covering on house
>
>Exterior2nd: Exterior covering on house (if more than one material)
>
>MasVnrType: Masonry veneer type
>
>MasVnrArea: Masonry veneer area in square feet
>
>ExterQual: Exterior material quality
>
>ExterCond: Present condition of the material on the exterior
>
>Foundation: Type of foundation
>
>BsmtQual: Height of the basement
>
>BsmtCond: General condition of the basement
>
>BsmtExposure: Walkout or garden level basement walls
>
>BsmtFinType1: Quality of basement finished area
>
>BsmtFinSF1: Type 1 finished square feet
>
>BsmtFinType2: Quality of second finished area (if present)
>
>BsmtFinSF2: Type 2 finished square feet
>
>BsmtUnfSF: Unfinished square feet of basement area
>
>TotalBsmtSF: Total square feet of basement area
>
>Heating: Type of heating
>
>HeatingQC: Heating quality and condition
>
>CentralAir: Central air conditioning
>
>Electrical: Electrical system
>
>1stFlrSF: First Floor square feet
>
>2ndFlrSF: Second floor square feet
>
>LowQualFinSF: Low quality finished square feet (all floors)
>
>GrLivArea: Above grade (ground) living area square feet
>
>BsmtFullBath: Basement full bathrooms
>
>BsmtHalfBath: Basement half bathrooms
>
>FullBath: Full bathrooms above grade
>
>HalfBath: Half baths above grade
>
>Bedroom: Number of bedrooms above basement level
>
>Kitchen: Number of kitchens
>
>KitchenQual: Kitchen quality
>
>TotRmsAbvGrd: Total rooms above grade (does not include bathrooms)
>
>Functional: Home functionality rating
>
>Fireplaces: Number of fireplaces
>
>FireplaceQu: Fireplace quality
>
>GarageType: Garage location
>
>GarageYrBlt: Year garage was built
>
>GarageFinish: Interior finish of the garage
>
>GarageCars: Size of garage in car capacity
>
>GarageArea: Size of garage in square feet
>
>GarageQual: Garage quality
>
>GarageCond: Garage condition
>
>PavedDrive: Paved driveway
>
>WoodDeckSF: Wood deck area in square feet
>
>OpenPorchSF: Open porch area in square feet
>
>EnclosedPorch: Enclosed porch area in square feet
>
>3SsnPorch: Three season porch area in square feet
>
>ScreenPorch: Screen porch area in square feet
>
>PoolArea: Pool area in square feet
>
>PoolQC: Pool quality
>
>Fence: Fence quality
>
>MiscFeature: Miscellaneous feature not covered in other categories
>
>MiscVal: $Value of miscellaneous feature
>
>MoSold: Month Sold
>
>YrSold: Year Sold
>
>SaleType: Type of sale
>
>SaleCondition: Condition of sale

# Getting Started

## Installation

<p align="justify">
Ensure that you have the necessary dependencies and a compatible environment. For this particular project, the code is run in a Google Colab environment. To run the code, you need to install the required packages. Run the following command to install the necessary packages (if not already installed):
</p>

```py
!pip install shap
```

```py
!pip install Kaggle
```

```py
!pip install optuna
```

## Import Libraries and Load Dataset

<p align="justify">
The first step is the upload your Kaggle API credentials. If running in a Google Colab environment such as this project, use the following command:
</p>

```py
from google.colab import files
files.upload()
```

Then download and unzip the dataset by running the below lines of code:

```py
!kaggle competitions download -c house-prices-advanced-regression-techniques
```

```py
!unzip /content/house-prices-advanced-regression-techniques.zip
```

<p align="justify">
Now, with the environment set up, the necessary libraries are imported and the Kaggle housing dataset is loaded for exploration, preprocessing, and eventually building the machine learning models.
</p>

```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from scipy.stats import norm

from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import LabelEncoder
from sklearn.metrics import mean_squared_error

import lightgbm as lgb
from lightgbm import LGBMRegressor
import xgboost as xgb
from xgboost import XGBRegressor

import shap
```

Finally, load the `train.csv` and `test.csv` files. An example is provided below:

```py
df_train = pd.read_csv('train.csv')
df_test = pd.read_csv('test.csv')
```

As the file names indicate, the train.csv file will be used for training and the test.csv file will be used for the trained model.

# Exploratory Data Analysis

<p align="justify">
The Exploratory Data Analysis (EDA) step plays an important role in understanding the dataset's underlying structure and characteristics - identifying patterns, relationships, and potential issues needing to be addressed prior to model training. Exploratory techniques are employed to gain insights into the distribution of the target variable <code>SalePrice</code>, view descriptive statistics, and identify the presence of missing values.
</p>

## Target Variable: `SalePrice` Distribution
Firstly, the distribution of `SalePrice` was plotted and its shape appeared to be akin to a positive-skewed (or right-skewed) distribution.

<p align="center">
<img src="/docs/img/target-distr.png">
</p>

## Descriptive Statistics

Then, descriptive statistics were displayed in order to reveal information on central tendency and spread of the numerical features. 

## Identifying Missing Values

Most importantly, measures were taken to detect missing values in the dataset. The below image displays the features with missing values:

<p align="center">
<img src="/docs/img/nullval.png">
</p>

By identifying the missing values, appropriate strategies can be devised to handle them. This will be discussed in the next section.

# Data Preprocessing

<p align="justify">
This next step is essential for ensuring data is cleaned, formatted, and structured in a way that facilitates the analysis process. Involved in this data preprocessing are handling missing values, encoding categorical features, and, if necessary, handling the distribution of the target variable `SalePrice`.
</p>

## Skewed Distribution

<p align="justify">
In general, a skewed distribution could greatly affect the model due to variability. Therefore, methods such as logarithmic transformations are applied to have the distributions approach a Normal distribution. Although LightGBM and XGBoost can handle skewed distributions quite well, in the case of <code>milestone-2</code>, logarithmic transformation on <code>SalePrice</code> was implemented in an attempt to discover possibilities of a noticeable difference in performance from the reduction of variability. Below you will find the new plot of `SalePrice` and will see how the distribution approaches a Normal distribution.
</p>

<p align="center">
<img src="/docs/img/target-log.png">
</p>

<p align="justify">
For <code>milestone-3</code>, however, there was no logarithmic transformation done for the target variable <code>SalePrice</code>. Details behind the reasoning will be provided in the section containing model evaluations.
</p>

## Missing Values and Categorical Features

<p align="justify">
Missing values aren't handled only because most algorithms do not support missing values, but also because missings values can introduce a loss of power. Strategies must be put into place for handling missing values appropriately. One such strategy that is used in this project is mean imputation, that is, for the numerical features. For categorical features (or features that contain non-numeric values), the text "missing" replaced the missing values.
</p>

<p align="justify">
Continuing on the topic of categorical features, it is necessary to encode them in order to convert them into respective numerical representations, most especially when an algorithm will be requiring numerical input. <code>LabelEncoder</code> was used to handle the encoding of the categorical features.
</p>

# Split Training and Test Sets

<p align="justify">
After completion of data cleaning and preprocessing comes another important step prior to building a model: splitting the dataset into training and test sets. The train-test split procedure is essential in the training of the model - allowing for evaluation of the model's performance on data that it has not yet been trained on. On one hand, the <code>train.csv</code> file will be used to train and develop the model and will be split into 70% training data and 30% test data. On the other hand, the <code>test.csv</code> file will be used after the model has been trained and for printing the house sale price predictions.
</p>

# Baseline

Both XGBoost and LightGBM models were utilized in `milestone-2` but only LightGBM was utilized for `milestone-3`.

## Baseline Model Training, Evaluation, and Predictions

<p align="justify">
The baseline models used were <code>LGBMRegressor</code> for LightGBM and <code>XGBRegressor</code> for XGBoost. Each of the models were initialized with the default hyperparameters with the exception of setting <code>random_state=123</code>. 5-fold cross-validation was implemented in the training process. The metrics used for evaluation of the model's performance after fitting were cross-validation ($CV$) scores, R-squared scores ($R^2$), and root mean square error ($RMSE$) scores.
</p>

Note: Recall that for `milestone-2`, a logarithmic transformation was implemented for `SalePrice` and is thus reflected in $RMSE$ scores.

<p align="justify">
Even with a log transformed <code>SalePrice</code>, there did not appear to be significant differences between each milestone's <code>LGBMRegressor</code> scores. There is, however, a noticeable difference, albeit small, in overall scores between <code>LGBMRegressor</code> and <code>XGBRegressor</code> where the LightGBM model performed better than the XGBoost model.
</p>

`milestone-2` scores:

<p align="center">
<img src="/docs/img/comparison.png">
</p>

`milestone-3` scores:

<p align="center">
<img src="/docs/img/baseline-eval.png">
</p>

Now, predictions can be made by utilizing the trained model on the `test.csv` data.

Note: To ensure that `SalePrice` reverted to its original formatting, an exponential transformation was implemented.

`milestone-2` predictions:

<p align="center">
<img src="/docs/img/lgbmr-pred.png">
</p>

<p align="center">
<img src="/docs/img/xgbr-pred.png">
</p>

`milestone-3` predictions:

<p align="center">
<img src="/docs/img/baseline-pred.png">
</p>

<p align="justify">
Looking at `Id` and `SalePrice` alone for the model's predictions will not provide sufficient information for understanding the underlying factors that impacted (or influenced) the resulting prediction on house sale price. Model interpretability is where SHapley Additive exPlanations plots come in (as you will see in the next section).
</p>

## Baseline SHAP Summary and Interaction Plots

<p align="justify">
Plotting SHapley Additive exPlanations (SHAP) values is a great method for model explainability. To be more specific, SHAP applies a game theory approach for explaining the output of a model with the ability to display both global and local explanations.
</p>

<p align="justify">
This documenation will not provide screenshots of each SHAP visualization plotted for both <code>milestone-2</code> and <code>milestone-3</code>, since displaying only the SHAP plots generated in <code>milestone-3</code> should be sufficient in the discussion of each of the different plots' use and interpretation. Refer to the links of the <code>Milestone 2 Documentation</code> and <code>Milestone 3 Documentation</code> located in the <code>README.md</code> of branch <code>milestone-4</code>.
</p>

<p align="justify">
The core explainer API that this project uses is <code>TreeExplainer</code>, since not only is it fast, it is well-suitable for computing SHAP values of tree-based models. The choice of having the explainer grab SHAP values from either the training set or test set is made for whichever data is preferred to be analyzed. The point of interest for this project, in particular, is to view the interpretations of the training set <code>X_train</code>. The <a href="https://github.com/GHcpv24/CS634-Data-Mining/blob/milestone-4/CS634_CVega_Notebook.ipynb">notebook</a>, however, does provide code (though commented out) to plot the SHAP values explaining the test set <code>X_test</code>. Feel free run the code for your interest.
</p>

- Bar plot
  
   <p align="justify">
   For LightGBM, the bar plot serves as feature importance plots, where the features are displayed on the left-hand side and ranked with the most influential feature at the top down to the least influential feature at the bottom. In this    particular case, however, the SHAP bar plot displays a maximum of 10 features - the bottom-most feature representing a sum of the remaining 71 features. The mean absolute SHAP values - the average magnitude of each feature's impact on    the model's predicted house <code>SalePrice</code> across all instances - determine the ranking of the features. Throughout the entirety of the project, the feature <code>OverallQual</code> was the most impactful, and is the case as illustrated by all the different plots. This is unsurprising given a reasonable expectation that a house's overall quality rating would have a significant impact on the sales price of the house in question.
   </p>

<p align="center">
<img src="/docs/img/bar1.png">
</p>

- Beeswarm plot

  <p align="justify">
   Beeswarm plots function similarly to the bar plots as you will find the feature importance ranking by most influential at the top down to the least influential at the bottom. The difference is that beeswarm plots provide additional information by displaying the relationship between the model's prediction and the relative feature importance. More specifically, you will find that the each SHAP value (each point) is distributed horizontally according to their respective SHAP value as well as stacked vertically to show the density of the SHAP values. Each of these points are assigned a color corresponding to the feature's raw values, with red indicating a high feature value and blue a low feature value. The directionality impact of each feature - the general relationship between the raw values and SHAP values - provide valuable insights by examining the color distribution.
  </p>

  <p align="justify">
   In the case of <code>OverallQual</code>, the feature with the highest impact for both models, a higher overall quality value leads to positive SHAP values indicating that a houses with high overall quality have higher sales prices predicted. Interestingly, for the XGBoost model in <code>milestone-2</code>, the feature <code>GarageType</code> has the reverse situation - where a lower <code>GarageType</code> value leads to higher house sales price prediction.
  </p>

<p align="center">
<img src="/docs/img/beeswarm1.png">
</p>

- Waterfall plot

  <p align="justify">
   The ability to provide a more detailed breakdown of each feature's contribution towards the prediction of house <code>SalePrice</code> makes waterfall plots great visualization tools. The waterfall structure places emphasis on the additive nature of the positive and negative impacts built on the base value $E[f(X)]$ (the expected value of the house sales price model output) for yielding the specified model's prediction $f(X)$. In other words, each feature depicts the direction of the positive (red) or negative (blue) contribution by which the values are moved from the expected model output over the dataset to the model prediction output. As an example, you will find that tThe top contributor, <code>OverallQual</code> "pushes" the prediction of the sale price to be low. This could be considered reasonable given that the year is 1996 and overall quality is 5.
  </p>

<p align="center">
<img src="/docs/img/waterfall1.png">
</p>

- Force plot

  <p align="justify">
   Force plots also illustrate the manner in which each feature "pushes" the model towards either a higher or lower <code>SalePrice</code>, but in a more condensed display. Again, the feature <code>OverallQual</code> can be found to be the most impactful as well as found to be "pushing" the prediction towards a lower sale price.
  </p>

<p align="center">
<img src="/docs/img/force1.png">
</p>

- Shap interaction plots

  <p align="justify">
   Below images display 2 different types of plots, however, both hone in on SHAP interaction values. The first type of plot shown is a dependence plot. The top 5 features contributing the most to the model's prediction (according to what was shown on the bar plots) were chosen to be examined for the dependence plots. In the first plot shown below, you can view the interaction effects of the features <code>OverallQuall</code> and <code>GrLivArea</code>, and each of the 5 dependence plots reveals interesting trends. The second type of plot displays the effects in the form of a matrix, with the main effects illustrated on the diagonal and the interaction effects illustrated on the off-diagonal. 
  </p>

<p align="center">
<img src="/docs/img/depend1-1.png">
</p>
<p align="center">
<img src="/docs/img/depend1-2.png">
</p>

<p align="center">
<img src="/docs/img/interact1.png">
</p>

# Hyperparameter Optimization via Optuna

## Tuned Model Training, Evaluation, and Predictions

## Tuned SHAP Summary and Interaction Plots

# HuggingFace Streamlit App

## App Results

# App Landing Page

# Demo

https://github.com/GHcpv24/CS634-Data-Mining/assets/106451112/39573996-deeb-4086-9a8b-6cf33b9397d9

# Conclusion

# References

The HuggingFace streamlit app created references [this](https://github.com/adhok/streamlit_ames_housing_price_prediction_app) app.
