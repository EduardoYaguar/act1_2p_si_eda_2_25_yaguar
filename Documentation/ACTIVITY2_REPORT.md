# Activity 2: Categorical Data Encoding and Feature Scaling Techniques

**Student:** Eduardo Yaguar
**Course:** Intelligent Systems  
**Project:** Patient Readmission to Hospital After Discharge  
**Date:** November 2025

---

## 1. Introduction

This report presents the application of categorical encoding techniques to the diabetes hospital readmission dataset. The goal is to improve the prediction model by properly handling categorical variables.

## 2. Encoding Techniques Applied

### 2.1 Label Encoding

**Description:** Converts categorical values into numerical labels (0, 1, 2, ..., n).

**Use Case:** Applied to ordinal variables where order matters.

**Applied to:**
- `age`: Age ranges ([0-10), [10-20), ..., [90-100))
- `insulin`: Dosage levels (No, Steady, Up, Down)

**Python Library:** `sklearn.preprocessing.LabelEncoder`

**Justification:** Age groups have natural ordering, and insulin changes represent different treatment intensities.

### 2.2 One-Hot Encoding

**Description:** Creates binary columns for each category value. Each column represents presence (1) or absence (0) of that category.

**Use Case:** Applied to nominal categorical variables without inherent order.

**Applied to:**
- `race`: Patient race categories
- `gender`: Male/Female
- `change`: Medication change (Yes/No)
- `diabetesMed`: Diabetes medication (Yes/No)

**Python Library:** `pandas.get_dummies()`

**Justification:** These variables have no natural ordering, so one-hot encoding prevents the model from assuming false relationships.

### 2.3 Binary Encoding

**Description:** Converts categories to binary numbers, then splits each digit into separate columns. More efficient than one-hot encoding for high-cardinality variables.

**Use Case:** Applied to variables with many categories.

**Applied to:**
- `admission_type_id`: 8 admission types
- `discharge_disposition_id`: 30 disposition types
- `admission_source_id`: 26 source types

**Python Library:** `category_encoders.BinaryEncoder`

**Justification:** These IDs have many categories. Binary encoding reduces dimensionality compared to one-hot encoding while preserving information.

## 3. Models Comparison

### 3.1 Model 1: Baseline (Without Encoding)

**Features:** Only numerical features (11 features)
- admission_type_id, discharge_disposition_id, admission_source_id
- time_in_hospital, num_lab_procedures, num_procedures
- num_medications, number_outpatient, number_emergency
- number_inpatient, number_diagnoses

**Algorithm:** Random Forest Classifier
- n_estimators: 100
- max_depth: 10
- class_weight: balanced

**Results:**
- Accuracy: 0.5142 (51.42%)
- F1-Score: 0.5206 (52.06%)

### 3.2 Model 2: With Encoding Techniques

**Features:** Numerical + encoded categorical features (32 features)
- All baseline numerical features
- Label encoded: age, insulin
- One-hot encoded: race, gender, change, diabetesMed
- Binary encoded: admission_type_id, discharge_disposition_id, admission_source_id

**Algorithm:** Random Forest Classifier (same parameters)

**Results:**
- Accuracy: 0.5269 (52.69%)
- F1-Score: 0.5286 (52.86%)

## 4. Results Analysis

### Performance Improvement

| Metric | Baseline | Encoded | Improvement |
|--------|----------|---------|-------------|
| Accuracy | 0.5142 | 0.5269 | +2.47% |
| F1-Score | 0.5206 | 0.5286 | +1.54% |

### Key Findings

1. **Positive Impact:** Encoding techniques improved both accuracy and F1-score.

2. **Feature Expansion:** The model went from 11 to 32 features, capturing more information from categorical variables.

3. **Modest Improvement:** The improvement is small but consistent across metrics, suggesting the encoding helps but the prediction task remains challenging.

4. **Balanced Performance:** F1-score improvement indicates better handling of imbalanced classes.

## 5. Techniques Explanation

### Why These Techniques?

- **Label Encoding:** Best for ordinal data (age groups, medication levels)
- **One-Hot Encoding:** Standard for nominal categories with few values
- **Binary Encoding:** Efficient for high-cardinality categorical variables

### Libraries Used

```python
from sklearn.preprocessing import LabelEncoder
from category_encoders import BinaryEncoder
import pandas as pd  # for get_dummies()
```

## 6. Conclusions

1. **Effectiveness:** Categorical encoding techniques improved model performance, with accuracy increasing by 2.47% and F1-score by 1.54%.

2. **Feature Engineering:** Properly encoding categorical variables allows the model to use more information, increasing features from 11 to 32.

3. **Technique Selection:** Different encoding methods were appropriate for different variable types:
   - Label encoding for ordinal variables
   - One-hot encoding for low-cardinality nominal variables
   - Binary encoding for high-cardinality variables

4. **Model Complexity:** Despite adding features, the Random Forest model handled the increased dimensionality well with balanced class weights.

5. **Future Work:** The modest improvement suggests that other factors (feature engineering, hyperparameter tuning, or different algorithms) might be needed for better performance.

6. **Practical Application:** For the hospital readmission prediction task, encoding techniques are meaningful and should be used, though they are not sufficient alone for high accuracy.

## 7. References

- Scikit-learn documentation: https://scikit-learn.org/stable/modules/preprocessing.html
- Category Encoders: https://contrib.scikit-learn.org/category_encoders/
- Pandas documentation: https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html
- Random Forest Classifier: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html

---

**End of Report**
