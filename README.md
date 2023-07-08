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

## Import Libraries and Load Dataset

To acquire the dataset, follow these steps:

1. Upload the required datasets (`train.csv` and `test.csv`) to your working environment.
2. Ensure that the datasets are in the correct format and accessible for the code to read.

## Exploratory Data Analysis

The code performs exploratory data analysis (EDA) to gain insights into the dataset. EDA includes the following steps:

- Visualizing the distribution of the target variable (`SalePrice`)

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/9bd3353f-2b23-4182-b000-53a0599fe47d)

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

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/fca7687f-60bd-460f-b6c8-73dea2fc80d3)

- Making predictions on the test dataset `test.csv`

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f88c5d86-7dda-4fef-915a-828a2ce90337)

## Feature Importance and Interaction Analysis using SHAP

Feature importance analysis is performed using the SHAP (SHapley Additive exPlanations) library. The code calculates SHAP values and interaction values for the models and visualizes feature importance using SHAP plots.

- Bar Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f3be8c91-52f1-46ac-aa30-44621bf7d380)

- Beeswarm Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/31e0d411-6ebe-44fe-8913-31c2c56c0bd7)

- Waterfall Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/a5e33883-61db-4789-8b0a-cd0f1e8ab974)

- Force Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/df0b62b2-16d8-4e22-9e6d-dba0ad3c5886)

 - SHAP Interactions

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/147add8d-2706-4007-aace-1611dd915fa7)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/9dbd3904-9bf9-4643-ac8a-f5159c48a6ee)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f65ddf9a-d2f4-4fa5-b5d5-8390703cac7e)

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

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/50d3e47a-820f-49b6-9792-62c2e62a1152)

- Prediction

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/11472cda-9f92-4bf9-b48f-d909d30398d5)

## SHAP for Optimized LightGBM Model

- Bar Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/bf151256-3dca-4fa6-83ce-79dc66213059)

- Beeswarm Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/11fc1529-8750-4ff5-9457-4f7e2d9a3bbc)

- Waterfall Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/0c729fc1-6efc-4a6a-a8ac-972a2d7b0e4b)

- Force Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/6ae920fc-b137-47fb-ada5-7f4d47900be1)

 - SHAP Interactions

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/dd298bdf-1547-4a44-baa3-3fb54c3207b0)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/ad426f3c-0c63-41e8-bbcd-b33ad1c7502e)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f214d3fb-0c3a-4804-be59-ecb429dc8718)

## Prepare for HuggingFace Streamlit App

Use `pickle` library to save trained baseline and trained optimized models

## HuggingFace Streamlit App Results

Example of results from using my LightGBM House Sale Price PRediction streamlit app on HuggingFace.

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/7bf0ef04-6ce0-4f6e-9cf8-b81ed0981497)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/78ff9f26-ed95-4cbc-95fc-8d84d23ec55e)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/bb2fd050-21f2-42d3-8df6-e3be2053640c)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f5b9589e-1ac8-496e-bab4-913e2cc7368b)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/90de9633-5469-4601-86a3-3c1f6351ab4d)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/d5f299cd-7c87-4f0b-81aa-e521364ca6da)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/4ceb4d16-cd4f-442c-9dc9-97224a57f219)

![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/dc23b262-eb85-4fff-8017-b0a3ea514acf)

## Conclusion

In conclusion, this code demonstrates the process of Milestone 3's house `SalePrice` price prediction. The LightGBM models had shown more improvements as indicated by a better cross-validation, $R^2$ and RMSE scores. SHAP plots again provide valuable insights into the significance of different features. Feel free to explore the code and experiment with different models and techniques to further improve the predictions.
