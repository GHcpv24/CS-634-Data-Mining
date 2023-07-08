# CS-634-Data-Mining

## Milestone 2: (Week 3, 40 points)

Download the dataset from [here](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)

[![Watch the video](https://img.youtube.com/vi/-taOhqkiuIo/0.jpg)](https://youtu.be/-taOhqkiuIo)

Read the [excellent summary on SHAP that Google engineers have put together](https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf). Watch the video and read the blog posts [here](https://towardsdatascience.com/interpretable-machine-learning-with-xgboost-9ec80d148d27) to understand the problem and its solution provided by [Tree SHAP](https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html). The blog post discusses the XGBoost implementation of gradient boosting but the concept is the same.

Perform the SHAP interpretation of the house price prediction model of your choice. At a minimum you should produce graphs that show the SHAP values for the features and the SHAP interaction values for these features.

---

# House Price Modeling using Regression Techniques for Prediction and SHAP for Explainability/Interpretability 

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
