# Toxicity Prediction using Molecular Descriptors

This repository contains a machine learning pipeline to predict chemical toxicity (**Toxic** vs. **Non-Toxic**) based on molecular descriptors. The project addresses the challenges of high-dimensional data and class imbalance using robust feature selection and ensemble modeling.

## 📌 Project Overview

The goal of this project is to build a binary classifier that identifies the toxicity class of chemical compounds. The dataset presents a "High Dimension, Low Sample Size" (HDLSS) problem, featuring over $1,200$ descriptors for only $171$ samples.

### Key Challenges:
- **Feature Redundancy:** Many chemical descriptors are highly correlated ($>0.95$).
- **Dimensionality:** The number of features ($p=1204$) significantly exceeds the number of observations ($n=171$).
- **Class Imbalance:** Non-Toxic samples ($104$) outnumber Toxic samples ($67$).

## 🛠️ Methodology

### 1. Exploratory Data Analysis (EDA)
- **Distribution Analysis:** Evaluated the balance between `Toxic` and `Non-Toxic` classes.
- **Null Value Inspection:** Confirmed a clean dataset with no missing values.
- **Statistical Profiling:** Analyzed the range and variance of molecular descriptors to understand feature scaling needs.

### 2. Data Preprocessing
- **Target Encoding:** Converted categorical labels (`NonToxic` $\rightarrow$ 0, `Toxic` $\rightarrow$ 1).
- **Constant Feature Removal:** Eliminated features with zero variance.
- **Multicollinearity Filter:** Removed $562$ features with a correlation coefficient $> 0.95$ to reduce redundancy and improve model stability.

### 3. Feature Selection
To prevent overfitting and the "Curse of Dimensionality," a model-based feature selection strategy was implemented:
- **Algorithm:** Random Forest Importance.
- **Selection:** Retained the top $50$ features based on their relative contribution to the model's Gini impurity reduction.

### 4. Modeling & Evaluation
- **Base Model:** Random Forest Classifier (Ensemble Model).
- **Class Handling:** Utilized `class_weight='balanced'` to ensure the model penalizes misclassifications of the minority (Toxic) class.
- **Validation:** 5-Fold Stratified Cross-Validation to ensure results are robust across different data subsets.
- **Metrics:** Tracked Accuracy, Precision, Recall, and F1-Score.

## 📊 Results Summary

| Metric | Score (Mean $\pm$ Std) |
| :--- | :--- |
| **Accuracy** | $64.32\% \pm 5.7\%$ |
| **Precision** | $41.33\% \pm 16.6\%$ |
| **Recall** | $18.03\% \pm 10.1\%$ |
| **F1-Score** | $24.33\% \pm 12.4\%$ |

**Top Predictors:** The most influential descriptors identified include `SpMAD_Dt`, `ZMIC1`, `SpAD_Dt`, and `MDEC-23`.

## 📁 Repository Structure

```text
├── data.csv                # Raw dataset containing molecular descriptors
├── toxicity_analysis.py    # Python script with full EDA and Modeling
├── README.md               # Project documentation
└── plots/                  # Generated visualizations
    ├── feature_importance.png
    ├── confusion_matrix.png
    └── class_distribution.png
