## Breast Cancer Recurrence Prediction

### Overview
This project develops and compares five models to predict breast cancer recurrence using nine clinical variables from patient records.
The dataset contains 286 observations, each labeled as eitherrecurrence-events or no-recurrence-events.

### Project Structure
```
breast-cancer-recurrence/
├── README.md
├── .gitignore
├── data/
│   ├── breast-cancer.data
│   └── breast-cancer.names
└── notebooks/
     ├── 01_EDA_Preprocessing.ipynb
     ├── 02_Models.ipynb
     ├── 03_Comparison.ipynb
     └── complete_pipeline.ipynb
```
    
### Dataset
- **Source:** Zwitter, M. & Soklic, M. (1988). Breast Cancer [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C51P4M.
- **Samples:** 286
- **Features:** 9 (all categorical)
- **Target:** binary (recurrence vs no-recurrence)
- **Class distribution:** ~70% no-recurrence, ~30% recurrence (imbalanced)

### Features
| Feature | Type | Description |
|---------|------|-------------|
| age | Ordinal | Patient age range |
| menopause | Nominal | Menopausal status (lt40, ge40, premeno) |
| tumor-size | Ordinal | Tumor size in mm (ranges) |
| inv-nodes | Ordinal | Number of positive axillary lymph nodes |
| node-caps | Nominal | Lymph node capsule involvement (yes/no) |
| deg-malig | Ordinal | Tumor malignancy grade (1-3) |
| breast | Nominal | Affected breast (left/right) |
| breast-quad | Nominal | Affected breast quadrant |
| irradiat | Nominal | Radiation therapy received (yes/no) |

### Models
| Model | Description |
|-------|-------------|
| Logistic Regression | Linear model with L2 regularization and GridSearchCV |
| Deep Neural Network | Keras sequential model with hyperparameter tuning via Keras Tuner |
| Random Forest | Ensemble of decision trees with SMOTE and GridSearchCV |
| SVM (sigmoid) | Support Vector Classifier with RandomizedSearchCV |
| XGBoost | Gradient boosting with SMOTEENN and GridSearchCV |

All models are evaluated using **Stratified K-Fold Cross-Validation (*k=10*)** to ensure fair comparison.

### Techniques
- **Class imbalance handling:** SMOTE, SMOTEENN, class weighting
- **Feature selection:** SelectKBest with mutual information and chi-squared
- **Hyperparameter tuning:** GridSearchCV, RandomizedSearchCV, Keras Tuner
- **Evaluation metrics:** Accuracy, Precision, Recall, F1-score (macro/weighted), AUC-ROC, Average Precision
- **Statistical testing:** Friedman test for model comparison

### How to Run

1. Clone the repository
```
git clone https://github.com/username/breast-cancer-recurrence.git
cd breast-cancer-recurrence
```
2. Install dependencies
```
pip install pandas numpy scikit-learn imbalanced-learn tensorflow keras-tuner xgboost matplotlib seaborn scipy
```
3. Run notebooks in order ($01\rightarrow 02\rightarrow 03$) because each one generates intermediate files used by the next, or else just run the file **complete_pipeline.ipynb** at once.
