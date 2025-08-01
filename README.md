# Parkinson’s Disease Telemonitoring: Vocal Biomarker Regression & Causal Inference

## Overview

This project explores the role of vocal biomarkers in predicting Parkinson’s Disease severity using machine learning and causal inference techniques. It uses the Parkinson's Telemonitoring dataset to build predictive models and estimate causal effects of vocal features on clinical outcomes.

## Motivation

Parkinson’s Disease affects vocal characteristics early in its progression. If we can use these features to remotely assess disease severity, we can improve accessibility and frequency of monitoring. This project was conducted to:

- Predict motor and total UPDRS scores using voice-based features.
- Identify vocal features with the strongest predictive power.
- Determine whether specific features have a causal effect on disease progression.

## Dataset

- Source: [UCI ML Repository – Parkinson’s Telemonitoring](https://archive.ics.uci.edu/ml/datasets/Parkinsons+Telemonitoring)
- Size: 5,875 voice recordings from 42 individuals
- Features: 16 vocal features + demographics (`age`, `sex`, `test_time`)
- Targets: `motor_UPDRS`, `total_UPDRS`

## Methodology

### Feature Exploration

- Normality checks using histograms, KDEs, and Q-Q plots
- Gender-wise analysis for separate PCA component selection
- Standardization using `StandardScaler`

### PCA-based Dimensionality Reduction

- PCA used to reduce multicollinearity and capture >97.5% variance
- Component count: 8 (males), 9 (females), based on explained variance plots

### Regression Models

Trained the following models on PCA-transformed data:

- Linear Regression
- Ridge and Lasso Regression
- Random Forest Regressor
- Gradient Boosting Regressor

Evaluation Metrics:

- RMSE  
- MAE  
- R² Score  

### Model Comparison

- Predictions plotted against actual scores for interpretability
- Separate models and visualizations by gender and UPDRS type

### Causal Inference with IPW

- Converted features to binary treatment using median split
- Used logistic regression to estimate propensity scores based on confounders
- Applied Inverse Probability Weighting (IPW) in weighted linear regression
- Reported:
  - ATE (Average Treatment Effect)
  - p-values
  - 95% confidence intervals

## Results Summary

| Feature      | ATE    | p-value | Causal Effect      |
|--------------|--------|---------|--------------------|
| PPE          | +2.38  | <0.001  | Strong Positive     |
| RPDE         | +1.55  | <0.001  | Positive            |
| HNR          | -2.61  | <0.001  | Strong Negative     |
| Jitter(%)    | +1.37  | <0.001  | Positive            |
| Shimmer      | +1.27  | <0.001  | Positive            |
| DFA          | -1.20  | <0.001  | Negative            |

- Ensemble models (Random Forest, Gradient Boosting) showed the best predictive performance.
- Linear models revealed interpretable relationships.
- Causal inference identified statistically significant effects for key vocal markers.

## Tools & Libraries

- Python (pandas, numpy, matplotlib, seaborn)
- scikit-learn (PCA, regression models)
- statsmodels (WLS regression)
- LogisticRegression for propensity scoring

## Future Work

- Temporal modeling using `test_time` as a sequential signal
- Use SHAP or LIME for local interpretability
- Explore DoWhy or CausalNex for structural causal modeling
- Integrate models into a simple web dashboard for telemonitoring

---
