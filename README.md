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

---

# Links

- [Kaggle Housing Prices Prediction Dataset](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)
- [HF Streamlit App](https://huggingface.co/spaces/HFcpv24/LightGBM-House-Sale-Price-Prediction)
- [Milestone 3 Documentation](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-3/docs/Milestone3Documentation.md)
- [Milestone 3 Notebook](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-3/CS634_CVega_Milestone3.ipynb)

---

- [Milestone 1 Documentation](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-1/README.md)
- [Milestone 2 Documentation](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-2/docs/Milestone2Documentation.md)
- [Milestone 4 Documentation](https://github.com/GHcpv24/CS-634-Data-Mining/blob/milestone-4/docs/Milestone4Documentation.md)

---

# LightGBM Optimization, Predictions, SHAP Interpretations, and HuggingFace Streamlit App Implementation 

## Introduction

The goal of Milestone 3 is to predict house sales price, i.e. `SalePrice` as done in Milestone 2 but to include hyperparameter optimization by tuning with Optuna. The dataset consists of over 79 features such as year, location, lot size, and several other housing qualities. Milestone 3, as indicated by the deliverables, will only utilize the LightGBM model for prediction. Analyses of feature importances and interactions using SHAP will be done for both the baseline LightGBM model and the LightGBM model tuned with Optuna.

Another requirement to be fulfilled for Milestone 3 is that a HuggingFace streamlit app must be created to generate the baseline model and tuned model predictions.

The HuggingFace Streamlit App can be found [here](https://huggingface.co/spaces/HFcpv24/LightGBM-House-Sale-Price-Prediction).

## Installation

Ensure that you have the necessary dependencies and a compatible environment. To run the code, you need to install the required packages. Run the following command to install the necessary packages (if not already installed):

```py
!pip install shap
```

```py
!pip install Kaggle
```

```py
!pip install optuna
```
