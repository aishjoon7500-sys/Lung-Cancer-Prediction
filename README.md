# Lung Cancer Prediction using Machine Learning

A machine learning project that explores a lung cancer survey dataset and builds classification models to predict whether a person is likely to have lung cancer based on demographic, lifestyle, and symptom data.

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Models and Results](#models-and-results)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Repository Structure](#repository-structure)
- [Limitations and Future Work](#limitations-and-future-work)
- [Disclaimer](#disclaimer)

## Overview

Early detection of lung cancer greatly improves treatment outcomes. This project analyses a survey-style dataset of patient attributes and symptoms, then trains and compares three classifiers:

- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier

## Dataset

The dataset (`lung_cancer_dataset.xlsx`) contains **309 records** (274 after removing duplicates) and **17 columns**, with no missing values.

| Feature | Description |
|---|---|
| `GENDER` | Male / Female |
| `AGE` | Age in years |
| `Age Group` | Binned age group (e.g. 40-55, 55-70, 70-90) |
| `SMOKING` | Smoker (1) / non-smoker (0) |
| `YELLOW_FINGERS` | Presence of yellow fingers |
| `ANXIETY` | Presence of anxiety |
| `PEER_PRESSURE` | Influenced by peer pressure |
| `CHRONIC DISEASE` | Has a chronic disease |
| `FATIGUE` | Experiences fatigue |
| `ALLERGY` | Has allergies |
| `WHEEZING` | Experiences wheezing |
| `ALCOHOL CONSUMING` | Consumes alcohol |
| `COUGHING` | Experiences coughing |
| `SHORTNESS OF BREATH` | Experiences shortness of breath |
| `SWALLOWING DIFFICULTY` | Difficulty swallowing |
| `CHEST PAIN` | Experiences chest pain |
| `LUNG_CANCER` | **Target** variable (YES / NO) |

Binary symptom/lifestyle features are encoded as 0/1.

> **Note:** the dataset file is read from a local path in the notebook. Place `lung_cancer_dataset.xlsx` in the project folder and update the path before running.

## Project Workflow

1. **Data loading**: read the Excel file with pandas.
2. **Data cleaning**: check for nulls, inspect dtypes, and drop duplicate rows.
3. **Exploratory data analysis**: visualise distributions and relationships with the target.
4. **Preprocessing**: drop `Age Group`, encode `GENDER` and `LUNG_CANCER` as categorical codes.
5. **Modelling**: train/test split, then train and evaluate three classifiers.
6. **Evaluation**: accuracy, precision, confusion matrix, and classification report.

## Exploratory Data Analysis

The notebook includes the following visualisations:

- Gender distribution (pie chart)
- Age distribution (histogram with KDE)
- Age group distribution (donut chart)
- Gender vs. lung cancer (count plot)
- Coughing status distribution and coughing vs. lung cancer
- Smoking status distribution and smoking vs. lung cancer
- Alcohol consumption distribution and alcohol consumption vs. lung cancer

## Models and Results

Each model uses a different train/test split, so results are not strictly comparable.

| Model | Test Split | Accuracy | Precision |
|---|---|---|---|
| Logistic Regression (`max_iter=1000`) | 40% (`random_state=2`) | 93.64% | 94.00% |
| Decision Tree | 35% (`random_state=42`) | 89.58% | 94.00%* |
| Random Forest (100 trees) | 30% (`random_state=42`) | 89.16% | 92.00% |

\*Precision for the positive class, from the classification report.

The Decision Tree is also visualised using `plot_tree`.

**Observation:** the dataset is imbalanced (far more `YES` than `NO` cases), so recall for the `NO` class is noticeably lower across models (e.g. 0.60 for Logistic Regression). Accuracy alone can therefore be misleading.

## Tech Stack

- Python 3
- pandas, NumPy
- Matplotlib, Seaborn
- scikit-learn
- openpyxl (for reading `.xlsx` files)
- Jupyter Notebook

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```

2. **Install dependencies**
   ```bash
   pip install pandas numpy seaborn matplotlib scikit-learn openpyxl jupyter
   ```

3. **Add the dataset**: place `lung_cancer_dataset.xlsx` in the project folder and update the file path in the notebook:
   ```python
   var = pd.read_excel("lung_cancer_dataset.xlsx")
   ```

4. **Run the notebook**
   ```bash
   jupyter notebook ML_project_1.ipynb
   ```

## Repository Structure

```
.
├── ML_project_1.ipynb        # Main notebook (EDA + modelling)
├── lung_cancer_dataset.xlsx  # Dataset
└── README.md
```

## Limitations and Future Work

- Small dataset (274 unique rows) and class imbalance limit generalisation.
- Use a consistent train/test split (or cross-validation) to compare models fairly.
- Address imbalance with SMOTE, class weights, or stratified splitting.
- Report recall, F1-score, and ROC-AUC alongside accuracy.
- Add hyperparameter tuning (GridSearchCV) and feature importance analysis.
- Try additional models such as SVM, KNN, or gradient boosting.

## Disclaimer

This project is for educational purposes only. It is not a medical diagnostic tool and must not be used to make clinical decisions.
