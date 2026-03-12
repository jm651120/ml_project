# 📊 To Grant or not to Grant: Multiclass Prediction of Compensation Benefits

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-FF6600?style=flat)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)

**Developed by:** Beatriz Fonseca, João Marques, Martim Tavares, Matilde Domingues, Rodrigo Miranda

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Repository Structure](#repository-structure)
3. [Methodology & Preprocessing](#methodology--preprocessing)
4. [Model Evaluation & Comparison](#model-evaluation--comparison)
5. [Results & Key Insights](#results--key-insights)
6. [Future Work](#future-work)

---

## Project Overview

Each year, the New York Workers' Compensation Board (WCB) processes thousands of workplace injury claims. This project leverages machine learning to predict the **Claim Injury Type** — a multiclass classification problem — with the goal of automating claims management and improving decision accuracy.

The primary challenge was a **severe class imbalance**: the majority class accounted for over 50% of claims, while minority classes (e.g., `PTD`, `DEATH`) represented less than 1% of the data. Our pipeline was built specifically to handle this real-world imbalance robustly.

---

## Repository Structure
```
├── Project Description.pdf               # Project goals, dataset descriptions, and evaluation criteria
├── Machine_Learning_Group43_Report.pdf   # Final report documenting methodology and analysis
├── Part 1 - Initial Inspection.ipynb     # Data type corrections and initial exploration
├── Part 2 - Visual Exploration.ipynb     # EDA, correlation heatmaps, and Cramér's V associations
├── Part 3 - PreProcess, Feature          # Custom preprocessing pipeline, feature selection,
│            Selection, Model.ipynb       # and model training
└── Part 4 - Open Ended Section.ipynb     # Analysis of intermediate variable prediction
                                          # (Agreement Reached) and its impact on the final model
```

---

## Methodology & Preprocessing

We engineered temporal and behavioral features and built a custom preprocessing pipeline using **scikit-learn**:

- **Outlier Handling (`ClipOutliersMulti`):** Identifies and caps extreme outliers using quantile thresholds.
- **Imputation (`SampleKNNImputer` & `ZeroFillImputer`):** Fills missing values using k-Nearest Neighbors for complex features, and zero-filling where absence carries logical meaning.
- **Encoding (`FrequencyEncoder` & `OneHotEncoder`):** Handles high-cardinality categorical variables via frequency encoding, and standard OHE for low-cardinality features.
- **Feature Selection:** An XGBoost-based selector reduced dimensionality and mitigated overfitting, retaining the optimal ~53 features.

---

## Model Evaluation & Comparison

All models were benchmarked using **Stratified 5-Fold Cross-Validation**. Given the severe class imbalance, **F1-Macro** was used as the evaluation metric to ensure minority classes were equally penalised.

| Model | Train F1-Macro | Val F1-Macro | Overfit (Train − Val) |
|---|---|---|---|
| **XGBoost** | **0.4534** | **0.4317** | **0.0217** |
| Decision Tree | 0.4444 | 0.4047 | 0.0397 |
| Bagging (DT) | 0.4230 | 0.4058 | 0.0172 |
| Neural Network (MLP) | 0.4156 | 0.4071 | 0.0085 |
| Random Forest | 0.4029 | 0.3246 | 0.0783 |
| Stacking Classifier | 0.3932 | 0.3903 | 0.0029 |
| Logistic Regression | 0.3762 | 0.3743 | 0.0019 |

---

## Results & Key Insights

- **Best Model:** XGBoost achieved the highest validation F1-Macro of **0.4317**. L1 (Lasso) and L2 (Ridge) regularisation were critical in reducing overfitting while maintaining generalisation.
- **Handling Imbalance:** Tree-based models generally outperformed Neural Networks, though all models struggled with extreme minority classes. SMOTE was tested but discarded due to severe overfitting.
- **Feature Importance:** `Average Weekly Wage` proved to be the single most influential feature for predicting claim injury type.
- **Intermediate Variable Testing:** Predicting `Agreement Reached` and feeding it into the main model did not improve the final F1 score, primarily due to the low variance of that feature.

---

## Future Work

- **Advanced Imbalance Techniques:** Explore class-weighted training, cost-sensitive learning, or alternative sampling methods beyond standard SMOTE.
- **Ensemble Approaches:** Investigate more complex blending strategies to better capture minority class patterns.
- **Deployment:** Deploy the best-performing XGBoost model as a REST API for use by WCB staff.
