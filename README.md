# Hospital Quality Analysis

# Table of Contents
- [Project Motivation](#Project-Motivation)
- [Data Source](#Data-Source)
- [Analysis Summary](#Analysis-Summary)
- [Key Findings](#Key-Findings)
- [Acknowledgments](#Acknowledgments)
  
# Project Motivation
Hospitals and other healthcare facilities report various metrics related to patient outcomes and quality of care. By comparing these metrics to national standards, stakeholders—such as hospital administrators, policymakers, and patients—can gauge performance and pinpoint areas needing improvement. This project leverages a publicly available dataset to explore these metrics and create a predictive model that classifies hospital performance relative to the national average.

# Data Source
Dataset Name: Complications and Deaths - Hospital

Provider: [Centers for Medicare & Medicaid Services (CMS)](https://data.cms.gov/provider-data/)

Link: [Complications_and_Deaths-Hospital.csv](https://data.cms.gov/provider-data/dataset/ynj2-r877#data-table)
Key columns include:

Measure ID / Measure Name: Identifies the performance measure.
Compared to National: Indicates if the hospital is “No Different,” “Better,” or “Worse” than the national rate.
Denominator / Score / Lower Estimate / Higher Estimate: Numeric columns for calculations and confidence intervals.
Facility & Location Info: Details such as Facility ID, Address, City, State, ZIP, etc.

# Analysis Summary
Data Cleaning

Removed rows where `Denominator` was “Not Applicable” or “Not Available.”
Converted relevant columns to numeric types (`Denominator`, `Score`, `Lower Estimate`, `Higher Estimate`).
Dropped the `Footnote `column due to excessive null values.
Exploratory Data Analysis (EDA)

Created bar plots for measure frequencies and a boxplot for `Score` by `Compared to National`.
Identified a severe class imbalance: ~96% of facilities are labeled “No Different.”
Feature Engineering

Encoded categorical columns (Measure ID, Measure Name, Compared to National) using `LabelEncoder`.
Optionally merged facility columns into a single text column (`Merged_Columns`).
Modeling

Used Logistic Regression with StratifiedKFold cross-validation to handle the class imbalance.
Compared a baseline logistic regression to a class-weighted one and observed the impact on minority class recall vs. overall accuracy.
Evaluation

Computed Accuracy, Precision, Recall, and F1 scores, focusing on macro-averaging due to imbalance.
Found that high accuracy is misleading given the skewed target distribution; the model improves minority-class recall at the cost of lower precision.

# Key Findings
Severe Class Imbalance: About 95–96% of rows are labeled “No Different Than the National Rate,” making it difficult for the model to correctly identify “Better” or “Worse” facilities.

Model Performance:

Baseline Logistic Regression: Very high accuracy (~95%) but near-zero recall for minority classes.

Class-Weighted Logistic Regression: Lower overall accuracy (~53–60%) but improved recall for minority classes.

Acknowledgments
Data:[Centers for Medicare & Medicaid Services (CMS)](https://data.cms.gov/provider-data/)

Tools & Libraries: - `Pandas`, `NumPy`, `scikit-learn`, `Matplotlib`, `Seaborn`.

