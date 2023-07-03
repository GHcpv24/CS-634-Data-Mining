# CS-634-Data-Mining

## Milestone 2: (Week 3, 40 points)

Download the dataset from [here](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)

[![Watch the video](https://img.youtube.com/vi/-taOhqkiuIo/0.jpg)](https://youtu.be/-taOhqkiuIo)

Read the [excellent summary on SHAP that Google engineers have put together](https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf). Watch the video and read the blog posts [here](https://towardsdatascience.com/interpretable-machine-learning-with-xgboost-9ec80d148d27) to understand the problem and its solution provided by [Tree SHAP](https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html). The blog post discusses the XGBoost implementation of gradient boosting but the concept is the same.

Perform the SHAP interpretation of the house price prediction model of your choice. At a minimum you should produce graphs that show the SHAP values for the features and the SHAP interaction values for these features.

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

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/97e3de3a-b2e1-4a5b-bbc8-67d54c6b52ce)

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

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/725be33f-6e94-4041-b4b3-656b5da07dd5)

- Making predictions on the test dataset `test.csv`

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/64d47472-279f-44b0-a414-602035fde586)

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/09f0de87-e561-4f2c-9273-bf26cc93d9b9)

## Feature Importance and Interaction Analysis using SHAP

Feature importance analysis is performed using the SHAP (SHapley Additive exPlanations) library. The code calculates SHAP values and interaction values for the models and visualizes feature importance using SHAP plots.

- Bar Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/f98e3f07-6c57-4e33-a5d9-94b8b02f0f85)

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/7a7732df-55d9-4c43-b6a1-abf1e141686e)

- Beeswarm Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/a5305971-2c68-4297-8f4d-72aedc0ab092)

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/9d997a40-8e94-4861-aa09-cd55a4b48a8f)

- Waterfall Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/370f7520-938c-49c8-b1cf-cb926138ccc0)

- Force Plots

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/c6cbc85c-92f4-4736-9747-76a13cc81df2)

  ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/961aa642-f474-4008-bbbe-7c3cf9a93ac8)

 - SHAP Interactions

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/858ef995-6dde-4ae2-84da-aa5bfb1e7f05)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/25b4d333-ee5b-4f61-847d-b450edd1f077)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/27cac91a-e6e2-4cc0-b350-1aaf46e5b859)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/9c2f3863-dcab-4f7f-964d-bce68c85d6ec)

   ![image](https://github.com/GHcpv24/CS-634-Data-Mining/assets/106451112/1f334d93-efb8-4701-967f-7af3ad9db8f0)

## Conclusion

In conclusion, this code demonstrates the process of Milestone 2's lhouse `SalePrice` price prediction. The LightGBM and XGBoost models perform quite well in predicting house prices, and the analysis using SHAP provides valuable insights into the significance of different features. Feel free to explore the code and experiment with different models and techniques to further improve the predictions.
