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
3. [Getting Started](#getting-started)

   3.1 [Installation](#installation)

   3.2 [Import Libraries and Load Dataset](#import-libraries-and-load-dataset)

4. [Exploratory Data Analysis](#exploratory-data-analysis)
5. [Data Preprocessing](#data-preprocessing)
6. [Baseline](#baseline)

   6.1 [Baseline Model Training and Evaluation](#baseline-model-training-and-evaluation)
   
   6.2 [Baseline SHAP Summary and Interaction Plots](#baseline-shap-summary-and-interaction-plots)

7. [Hyperparameter Optimization via Optuna](#hyperparameter-optimization-via-optuna)

   7.1 [Tuned Model Training and Evaluation](#tuned-model-training-and-evaluation)

   7.2 [Tuned SHAP Summary and Interaction Plots](#tuned-shap-summary-and-interaction-plots)

8. [HuggingFace Streamlit App](#huggingface-streamlit-app)

   8.1 [App Results](#app-results)

9. [App Landing Page](#app-landing-page)
10. [Demo](#demo)
11. [Conclusion](#conclusion)
12. [References](#references)

# Abstract

<p align="justify">
Provided within this documentation are extensive accounts of my methodology, findings, and insightss. The Interpretable Gradient Boosting - Real Estate House Price Prediction Project leveraged machine learning techniques to develop a predictive model and interpretable framework that can accurately predict housing sales prices based on various Ames, Iowa housing features (79 to be exact) such as year built, area square footage, number of bedrooms, etc. In <code>`milestone-1`</code>, the task was to get familiar with <code>`Docker`</code>. The machine learning model and SHapley Additive exPlanations (SHAP) plots were built in <code>`milestone-2`</code>, whereas <code>`milestone-3`</code> built upon the previous milestone by performing hyperparamter optimization with Optuna and added the creating of the HuggingFace streamlit app. For the final milestone, <code>`milestone-4`</code>, the task was to finalize the project by means of extensive documentation, creating a Google Sites landing page for the streamlit app, and producing a demo video of the app.
</p>

# Introduction

<p align="justify">
Due to the sheer variety and number of factors that affect house pricing, determining the sale price of a house if often challenging - a problem faced by realtors, homeowners, and buyers alike. The <a href"https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview">Kaggle Housing Prices Prediction Dataset</a> featuring data on Ames, Iowa homes, originally prepared by Dean De Cock, comprises 4 files: <code>`data_description.txt`</code>, <code>`sample_submission.csv`</code>, <code>`train.csv`</code>, and <code>`test.csv`</code>. Contained within the dataset are 79 explanatory variables and a little over 2.9k observations. The project aims to build a machine learning model that, based on the dataset, can predict the sale price of a house - being aware that machine learning can offer promising solutions to tackle the prediction challenge and task at hand. The models utilized in this project are LightGBM and XGBoost, whereas SHAP plots are used for interpretable (or explainable) machine learning. Optimization will be explored as well as the development of the HuggingFace streamlit app which provides an interface for users to experiment with the trained models. Prior to taking on these steps, however, are the Exploratory Data Analysis (EDA) and data preprocessing steps, which will be discussed shortly.
</p>

# Getting Started

## Installation

<p align="justify">
Ensure that you have the necessary dependencies and a compatible environment. To run the code, you need to install the required packages. Run the following command to install the necessary packages (if not already installed:
</p>

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

# Exploratory Data Analysis

# Data Preprocessing

# Baseline

## Baseline Model Training and Evaluation

## Baseline SHAP Summary and Interaction Plots

# Hyperparameter Optimization via Optuna

## Tuned Model Training and Evaluation

## Tuned SHAP Summary and Interaction Plots

# HuggingFace Streamlit App

## App Results

# App Landing Page

# Demo

https://github.com/GHcpv24/CS634-Data-Mining/assets/106451112/39573996-deeb-4086-9a8b-6cf33b9397d9

# Conclusion

# References

The HuggingFace streamlit app created references [this](https://github.com/adhok/streamlit_ames_housing_price_prediction_app) app.
