# Milestone 2

---

# House Price Modeling using Regression Techniques for Prediction and SHAP for Explainability/Interpretability 

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Import Libraries and Load Dataset](#import-libraries-and-load-dataset)
4. [Exploratory Data Analysis](#exploratory-data-analysis)
5. [Data Preprocessing](#data-preprocessing)
6. [Model Training and Evaluation](#model-training-and-evaluation)
7. [Feature Importance and Interaction Analysis using SHAP](#feature-importance-and-interaction-analysis-using-shap)
8. [Conclusion](#conclusion)

## Introduction

The goal of Milestone 2 is to predict house sales price, i.e. `SalePrice`. The dataset consists of over 79 features such as year, location, lot size, and several other housing qualities. Milestone 2 utilizes the LightGBM and XGBoost models for prediction and analyzes feature importance and interactions using SHAP.

## Installation

Ensure that you have the necessary dependencies and a compatible environment. To run the code, you need to install the required packages. Run the following command to install the necessary packages (if not already installed:

```
!pip install shap
```

```
!pip install Kaggle
```

## Import Libraries and Load Dataset

To acquire the dataset, follow these steps:

1. Upload the required datasets (`train.csv` and `test.csv`) to your working environment.
2. Ensure that the datasets are in the correct format and accessible for the code to read.

## Exploratory Data Analysis

The code performs exploratory data analysis (EDA) to gain insights into the dataset. EDA includes the following steps:

- Visualizing the distribution of the target variable (`SalePrice`)

  <p align="center">
  <img src="/docs/img/target-distr.png">
  </p>

- Looking at general information and descriptive statistics
- Checking for missing values

## Data Preprocessing

Data preprocessing is a crucial step before model training. The code performs the following preprocessing steps:

- Handling the target variable `SalePrice` distribution skew
- Handling missing values in both categorical and numerical features
- Encoding categorical features using label encoding

## Model Training and Evaluation

The code trains and evaluates the LightGBM and XGBoost regression models. The steps involved are:

- Splitting the `train.csv` dataset into training and validation sets (70% training and 30% validation
- Training the models on the training set
- Evaluating model performance using cross-validation and metrics

  <p align="center">
  <img src="/docs/img/comparison.png">
  </p>
  
- Making predictions on the test dataset `test.csv`

  <p align="center">
  <img src="/docs/img/lgbmr-pred.png">
  </p>

  <p align="center">
  <img src="/docs/img/xgbr-pred.png">
  </p>

## Feature Importance and Interaction Analysis using SHAP

Feature importance analysis is performed using the SHAP (SHapley Additive exPlanations) library. The code calculates SHAP values and interaction values for the models and visualizes feature importance using SHAP plots.

- Bar Plots

  <p align="center">
  <img src="/docs/img/bar1.png">
  </p>

  <p align="center">
  <img src="/docs/img/bar2.png">
  </p>

- Beeswarm Plots

  <p align="center">
  <img src="/docs/img/beeswarm1.png">
  </p>

  <p align="center">
  <img src="/docs/img/beeswarm2.png">
  </p>

- Waterfall Plots

  <p align="center">
  <img src="/docs/img/waterfall.png">
  </p>

- Force Plots

  <p align="center">
  <img src="/docs/img/lgbmr-force.png">
  </p>

  <p align="center">
  <img src="/docs/img/xgbr-force.png">
  </p>

 - SHAP Interactions

  <p align="center">
  <img src="/docs/img/lgbmr-depend1.png">
  </p>

  <p align="center">
  <img src="/docs/img/lgbmr-depend2.png">
  </p>

  <p align="center">
  <img src="/docs/img/xgbr-depend1.png">
  </p>

  <p align="center">
  <img src="/docs/img/xgbr-depend2.png">
  </p>

  <p align="center">
  <img src="/docs/img/interaction.png">
  </p>

## Conclusion

In conclusion, this code demonstrates the process of Milestone 2's lhouse `SalePrice` price prediction. The LightGBM and XGBoost models perform quite well in predicting house prices, and the analysis using SHAP provides valuable insights into the significance of different features. Feel free to explore the code and experiment with different models and techniques to further improve the predictions.
