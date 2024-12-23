# Machine-Learning: To Grant or not to Grant: Deciding on Compensation Benefits

## Project Developed By:
- Beatriz Fonseca
- João Marques
- Martim Tavares
- Matilde Domingues
- Rodrigo Miranda

---

## Table of Contents
- [Workplace Injury Claim Prediction Project](#workplace-injury-claim-prediction-project)
- [Repository Structure](#repository-structure)
- [Model Comparison Table](#model-comparison-table)
- [Workflow: Preprocessing Pipeline](#workflow-preprocessing-pipeline)
- [Results Summary](#results-summary)
- [Future Work](#future-work)
- [Data Access Note](#data-access-note)
- [Acknowledgments](#acknowledgments)

---

## Workplace Injury Claim Prediction Project

Each year, the **New York Workers' Compensation Board (WCB)** processes thousands of workplace injury claims. These claims are often reviewed manually, leading to inefficiencies, delays, and inconsistencies that can impact injured workers and burden the WCB with additional costs. 

This project seeks to revolutionize claims management by leveraging machine learning to provide a scalable, efficient, and accurate solution. Our goals are to:
- Automate the classification of injury claims.
- Improve the consistency and accuracy of decisions.
- Reduce manual effort in claims management.
- Provide valuable insights into the factors influencing claim outcomes.

---

## Repository Structure

- **Project Description.pdf**: Comprehensive documentation of the project goals, dataset descriptions, and evaluation criteria.
- **Machine_Learning_Group43_Report.pdf**: Final report with every step documented and deep analysis of the work done in our notebooks
- **Part 1 - Initial Inspection.ipynb**: Initial exploration of the dataset.
- **Part 2 - Visual Exploration.ipynb**: Comprehensive Exploratory Data Analysis (EDA) focusing on visualizations to uncover patterns, relationships, and distributions in the data.
- **Part 3 - PreProcess, Feature Selection, Model.ipynb**: Implementation of preprocessing steps, feature selection, and model development.
- **Part 4 - Open Ended Section.ipynb**: Analysis of how predicting the intermediate variable (*Agreement Reached*) impacts the performance of the final model.

---

## Model Comparison Table

The table below summarizes the performance of different machine learning models used in this project. The metrics include F1 Macro scores for training and validation datasets, as well as the difference between the two.

| F1 Macro       | XGBoost | Neural Networks | Decision Tree | Bagging | Logistic Regression | Random Forest | Stacking |
|----------------|---------|-----------------|---------------|---------|---------------------|---------------|----------|
| **train**      | 0.4534  | 0.4156          | 0.4444        | 0.4230  | 0.3762              | 0.4029        | 0.3932   |
| **val**        | 0.4317  | 0.4071          | 0.4047        | 0.4058  | 0.3743              | 0.3246        | 0.3903   |
| **train - val**| 0.0217  | 0.0085          | 0.0397        | 0.0172  | 0.0019              | 0.0783        | 0.0029   |

---

## Workflow: Preprocessing Pipeline

The preprocessing pipeline used in this project includes the following steps, ensuring the data is clean, standardized, and ready for modeling:
- **ClipOutliersMulti**: Identifies and caps extreme outliers to reduce their influence on model training.
- **MinMaxScaler**: Scales numeric features to a range between 0 and 1, improving model convergence.
- **OneHotEncoder**: Converts categorical variables into binary vectors for compatibility with machine learning models.
- **FrequencyEncoder**: Encodes high-cardinality categorical variables based on the frequency of each category.
- **SampleKNNImputer**: Fills missing values using k-Nearest Neighbors, ensuring imputation reflects data patterns.
- **ConvertDataType**: Ensures all variables are in the correct data type for analysis and modeling.
- **FixCodes**: Corrects inconsistencies in categorical code features, such as 'Gender' or 'Zip Code'.
- **ZeroFillImputer**: Replaces missing numeric values with zero, particularly for variables where absence has a logical meaning.
- **CodeMapper**: Maps categorical codes according to WCB documentation.

---

## Results Summary

- The XGBoost model achieved the highest validation F1 Macro score of **0.4317**, showing its strength in handling class imbalance and feature complexities.
- Predicting the intermediate variable (*Agreement Reached*) didn't show improvement because the class '1' was badly predicted.
- The feature 'Average Weekly Wage' showed to be the most influential in claims predictions

---

## Future Work

While the project achieved promising results, there are several opportunities for improvement and expansion:
- Incorporate additional feature selection methods to refine the model and identify the most impactful predictors.
- Integrate real-time data to enable dynamic predictions for incoming claims.
- Deploy the best-performing model as an API or web application for easy access and usability by WCB staff.

---

## Data Access Note

The dataset used in this project is too large to be included in this repository. For access to the data, please contact any of the project members listed above.

---

## Acknowledgments

We would like to thank:
- **Professor Ricardo Santos** for guidance and feedback throughout the project.
- Open-source libraries such as **scikit-learn**, **pandas**, and **matplotlib** for their contributions to this analysis.
---

We hope this repository serves as a valuable resource for understanding and applying machine learning to real-world problems. Feel free to contact any of the team members for questions, feedback, or collaborations!

