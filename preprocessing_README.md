# Preprocessing File Guide

This folder contains the preprocessing notebooks and intermediate datasets used to clean, aggregate, and merge the Home Credit application data. The notebooks should be read or executed in the order listed below.

## Notebook Order

### 1. `preprocess_current_updated.ipynb`

This notebook cleans the current application data. It handles correlated features, structural missing values, special categorical values, and basic feature filtering. The output of this notebook is the cleaned current application dataset.

**Main output:**
- `X_current_clean.csv`

---

### 2. `current_imputation.ipynb`

This notebook applies imputation to the cleaned current application data. Numerical variables are imputed using mean values, categorical variables are imputed using the most frequent category, and missing-value indicators are created when needed.

**Main output:**
- `df_current_imputed.csv`

---

### 3. `prev_eda.ipynb`

This notebook explores the previous application data, especially missing-value patterns related to contract status and application process stages. The analysis helps determine which missing values should be treated as structural rather than ordinary missing values.

---

### 4. `prev_new_features.ipynb`

This notebook creates new features for the previous application data before aggregation. These include amount ratios, timing-related variables, and other features designed to describe each previous application more informatively.

**Main output:**
- `prev_with_new_features.csv`

---

### 5. `prev_merged_by_person.ipynb`

This notebook aggregates the previous application data from the application-record level to the applicant level using `SK_ID_CURR`. Numerical variables are summarized using statistics such as mean, median, minimum, and maximum. Categorical variables are summarized using the most frequent category, its proportion, and the number of unique categories.

**Main outputs:**
- `prev_agg.csv`
- `prev_agg_feature_names.txt`

---

### 6. `merge.ipynb`

This notebook merges the imputed current application data with the aggregated previous application features. The current application table is used as the main table, and previous application features are joined by `SK_ID_CURR`.

**Main output:**
- Final modeling dataset

---

## Intermediate Data Folder

The folder `intermediate_data/` stores temporary datasets generated during preprocessing. These files are used to connect different notebooks and avoid rerunning earlier preprocessing steps.

| File name | Description |
|---|---|
| `X_current_clean.csv` | Cleaned current application data before imputation |
| `df_current_imputed.csv` | Current application data after imputation |
| `df_previous_filtered.csv` | Filtered previous application data used for further processing |
| `prev_with_new_features.csv` | Previous application data with newly constructed features |
| `prev_agg.csv` | Applicant-level aggregated previous application features |
| `prev_agg_feature_names.txt` | List of feature names created from previous application aggregation |
