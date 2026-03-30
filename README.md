# Fraud Detection ML Project

## Overview

This project builds a machine learning model to detect fraudulent credit card transactions using tabular data and scikit-learn.

The goal is to go beyond basic modeling by addressing real-world challenges such as **class imbalance** and **precision-recall tradeoffs**, rather than relying solely on accuracy.

---

## Problem Statement

Fraud detection is a highly imbalanced classification problem where fraudulent transactions are extremely rare but critical to detect.

A naive model can achieve high accuracy by predicting all transactions as non-fraud, but this fails to detect actual fraud cases.

---

## Dataset

* Credit Card Fraud Detection dataset
* ~284,807 transactions
* Target variable: `Class`

  * `0` → Normal
  * `1` → Fraud
* Highly imbalanced:

  * ~99.8% normal
  * ~0.2% fraud

---

## Approach

### 1. Data Exploration

* Loaded dataset using pandas
* Verified no missing values
* Identified extreme class imbalance

### 2. Baseline Model

* Logistic Regression (scikit-learn)
* Observed high accuracy but poor fraud detection

### 3. Handling Class Imbalance

* Applied `class_weight='balanced'`
* Improved fraud recall significantly

### 4. Threshold Tuning

* Used predicted probabilities instead of default threshold (0.5)
* Tested multiple thresholds to balance precision and recall

### 5. Model Comparison

* Compared Logistic Regression and Random Forest
* Evaluated models using ROC-AUC and classification metrics

---

## Results

## Logistic Regression
  
  * ROC-AUC: ~0.98
  * High recall with threshold tuning (~0.92)
  * Lower precision depending on threshold

## Random Forest
  
  * ROC-AUC: ~0.95
  * Precision: ~0.99 (very few false positives)
  * Recall: ~0.76

## Threshold Tuning Insights
  
  * Lower thresholds → higher recall, lower precision
  * Higher thresholds → higher precision, lower recall

# Example (Random Forest):

  * Threshold 0.9 → Precision: 1.00, Recall: 0.38
    * Demonstrates that maximizing precision can severely reduce recall

---

## Precision-Recall Curve

![Precision-Recall Curve Comparison](pr_curve_comparison.png)

The precision-recall curves for Logistic Regression and Random Forest largely overlap, indicating that both models have similar ability to rank fraudulent transactions.

However, differences emerge at specific thresholds:
  
  * Precision and recall are more meaningful metrics for fraud detection
  * Logistic Regression provides greater flexibility for recall optimization
  * Random Forest achieves higher precision at stricter thresholds
  * Class weighting significantly improves fraud recall
  * Model selection depends on business goals (recall vs precision tradeoff)

This highlights that model differences are more apparent in threshold behavior than overall ranking performance

---

## Key Learnings

* Identified severe class imbalance (~0.2% fraud)
* Baseline model achieved high accuracy (~99%) but poor fraud detection
* Applied class weighting to improve recall from ~56% → ~92%
* Tuned classification thresholds to balance precision and recall
* Demonstrated tradeoffs using precision-recall curve

---

## Why This Matters

In real-world fraud detection systems, missing fraudulent transactions is significantly more costly than false positives. 
This project demonstrates how model evaluation and threshold tuning must align with business objectives rather than relying on accuracy alone.

---

## Tech Stack

* Python
* pandas
* scikit-learn
* matplotlib
* Jupyter Notebook

---

## Project Structure

```
fraud-detection-ml/
├── data/
├── notebooks/
│   └── eda.ipynb
├── src/
├── README.md
└── requirements.txt
```

---

## Future Work

* Tune Random Forest thresholds for improved recall
* Explore advanced models (Gradient Boosting, XGBoost)
* Add feature engineering
* Integrate model with Personal Finance API for real-time fraud detection
