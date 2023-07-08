---
title: LightGBM House Sale Price Prediction
emoji: 🏆
colorFrom: pink
colorTo: purple
sdk: streamlit
sdk_version: 1.21.0
app_file: app.py
pinned: false
---

# CS-634-Data-Mining

## Milestone 3: (Week 4, 30 points)

Merge the earlier branch into the main branch and create a new branch titled ‘milestone-3. Do not delete the milestone-2 branch.

Repeat the analysis in Milestone 2 but this time use [this](https://towardsdatascience.com/kagglers-guide-to-lightgbm-hyperparameter-tuning-with-optuna-in-2021-ed048d9838b5) or [this](https://neptune.ai/blog/lightgbm-parameters-guide) guide to tune with [Optuna](https://optuna.org/) the hyperparameters of the LightGBM model.

You need to creating a streamlit app for the house price prediction problem. Streamlit is a python library that allows you to create web apps with minimal coding and deploy them in the cloud. Deploy the streamlit app in [HuggingFace streamlit spaces](https://huggingface.co/docs/hub/spaces-sdks-streamlit) after you create a free account. The app must resemble [this UI](https://adhok-streamlit-ames-housing-price-predict-streamlit-app-lp8hyj.streamlit.app/) (please avoid the shown gif image) and in addition it must show a SHAP summary plot and a SHAP interaction plot.

Submit the github repository URL with a branch titled ‘milestone-3’ with the [README.md]() file containing the link to the deployed HF space where the Milestone 2 calculation and the optimized app calculation price prediction can both be seen.

# House Price Modeling using Regression Techniques for Prediction and SHAP for Explainability/Interpretability 

## Links

- [Kaggle Housing Prices Prediction Dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)
- [HF Streamlit App](https://huggingface.co/spaces/HFcpv24/LightGBM-House-Sale-Price-Prediction)
- [Milestone 3 Notebook](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-3/CS634_CVega_Milestone3.ipynb)

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Import Libraries and Load Dataset](#import-libraries-and-load-dataset)
4. [Exploratory Data Analysis](#exploratory-data-analysis)
5. [Data Preprocessing](#data-preprocessing)
6. [Model Training and Evaluation](#model-training-and-evaluation)
7. [Feature Importance and Interaction Analysis using SHAP](#feature-importance-and-interaction-analysis-using-shap)
8. [Hyperparameter Optimization via Optuna](#hyperparameter-optimization-via-optuna)
9. [Tuned Model Training and Evaluation](#tuned-model-training-and-evaluation)
10. [SHAP for Optimized LightGBM Model](#shap-for-optimized-lightgbm-model)
11. [Prepare for HuggingFace Streamlit App](#prepare-for-huggingface-streamlit-app)
12. [HuggingFace Streamlit App Results](#huggingface-streamlit-app-results)
13. [Conclusion](#conclusion)

## Introduction

The goal of Milestone 3 is to predict house sales price, i.e. `SalePrice` as done in Milestone 2 but to include hyperparameter optimization by tuning with Optuna. The dataset consists of over 79 features such as year, location, lot size, and several other housing qualities. Milestone 3, as indicated by the deliverables, will only utilize the LightGBM model for prediction. Analyses of feature importances and interactions using SHAP will be done for both the baseline LightGBM model and the LightGBM model tuned with Optuna.

Another requirement to be fulfilled for Milestone 3 is that a HuggingFace streamlit app must be created to generate the baseline model and tuned model predictions.

The HuggingFace Streamlit App can be found [here](https://huggingface.co/spaces/HFcpv24/LightGBM-House-Sale-Price-Prediction).

## Installation

Ensure that you have the necessary dependencies and a compatible environment. To run the code, you need to install the required packages. Run the following command to install the necessary packages (if not already installed:

```
!pip install shap
```

```
!pip install Kaggle
```

```
!pip install optuna
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

- Handling missing values in both categorical and numerical features
- Encoding categorical features using label encoding

## Model Training and Evaluation

The code trains and evaluates the LightGBM and XGBoost regression models. The steps involved are:

- Splitting the `train.csv` dataset into training and validation sets (70% training and 30% validation
- Training the models on the training set
- Evaluating model performance using cross-validation and metrics

  <p align="center">
  <img src="/docs/img/baseline-eval.png">
  </p>
  
- Making predictions on the test dataset `test.csv`

  <p align="center">
  <img src="/docs/img/baseline-pred.png">
  </p>
  
## Feature Importance and Interaction Analysis using SHAP

Feature importance analysis is performed using the SHAP (SHapley Additive exPlanations) library. The code calculates SHAP values and interaction values for the models and visualizes feature importance using SHAP plots.

- Bar Plot

  <p align="center">
  <img src="/docs/img/bar1.png">
  </p>
  
- Beeswarm Plot

  <p align="center">
  <img src="/docs/img/beeswarm1.png">
  </p>
  
- Waterfall Plot

  <p align="center">
  <img src="/docs/img/waterfall1.png">
  </p>
  
- Force Plot

  <p align="center">
  <img src="/docs/img/force1.png">
  </p>
  
 - SHAP Interactions

  <p align="center">
  <img src="/docs/img/depend1-1.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/depend1-2.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/interact1.png">
  </p>
  
## Hyperparameter Optimization via Optuna

Perform tuning on the following hyperparameters:

```
params_lgbm = {
        'n_estimators': trial.suggest_int('n_estimators', 100, 1000),
        'learning_rate': trial.suggest_float('learning_rate', 0.01, 0.1),
        'max_depth': trial.suggest_int('max_depth', 3, 10),
        'num_leaves': trial.suggest_int('num_leaves', 10, 100),
        'min_child_samples': trial.suggest_int('min_child_samples', 1, 20),
        'subsample': trial.suggest_float('subsample', 0.5, 1.0),
        'colsample_bytree': trial.suggest_float('colsample_bytree', 0.5, 1.0),
    }
```

## Tuned Model Training and Evaluation

- Evaluation

  <p align="center">
  <img src="/docs/img/tuned-eval.png">
  </p>
  
- Prediction

  <p align="center">
  <img src="/docs/img/tuned-pred.png">
  </p>
  
## SHAP for Optimized LightGBM Model

- Bar Plot

  <p align="center">
  <img src="/docs/img/bar2.png">
  </p>
  
- Beeswarm Plot

  <p align="center">
  <img src="/docs/img/beeswarm2.png">
  </p>
  
- Waterfall Plot

  <p align="center">
  <img src="/docs/img/waterfall2.png">
  </p>
  
- Force Plot

  <p align="center">
  <img src="/docs/img/force2.png">
  </p>
  
 - SHAP Interactions

  <p align="center">
  <img src="/docs/img/depend2-1.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/depend2-2.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/interact2.png">
  </p>
  
## Prepare for HuggingFace Streamlit App

Use `pickle` library to save trained baseline and trained optimized models

## HF LightGBM House Sale Price Prediction Streamlit App

The HuggingFace `LightGBM-House-Sale-Price-Prediction` streamlit app provides an interactive and user-friendly interface with sliders allowing the user to select various housing details (i.e. year, # of beds, etc.). Once the user has made their selections, a button can be clicked to generate the LightGBM baseline and LightGBM tuned models' predictions for the house sales price based on the chosen slider parameters.

### App Preview:

  <p align="center">
  <img src="/docs/img/app_preview.png">
  </p>

### App Example Results

- Baseline LightGBM Predictions
  <p align="center">
  <img src="/docs/img/app_base1.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/app_base2.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/app_base3.png">
  </p>

- Tuned LightGBM Predictions
  <p align="center">
  <img src="/docs/img/app_tuned1.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/app_tuned2.png">
  </p>
  
  <p align="center">
  <img src="/docs/img/app_tuned3.png">
  </p>
  
## Conclusion

In conclusion, this code demonstrates the process of Milestone 3's house `SalePrice` price prediction. The LightGBM models had shown more improvements as indicated by a better cross-validation, $R^2$ and RMSE scores. SHAP plots again provide valuable insights into the significance of different features. Feel free to explore the code and experiment with different models and techniques to further improve the predictions.
