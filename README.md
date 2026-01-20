# Credit Risk Prediction Projects

This repository contains two complementary projects for credit risk assessment using different methodologies:

1. **Credit Risk Prediction** (`credit_risk/`) - Modern Machine Learning approach
2. **Credit Scoring Model** (`scoring/`) - Traditional credit scoring with WoE transformation

---

## Project 1: Credit Risk Prediction (`credit_risk/`)

### Overview
Predicts loan default risk using standard machine learning classification models. This approach focuses on maximizing predictive performance using modern ML algorithms.

### Methods Used

#### Data Preprocessing
1. **Missing Value Handling**
   - `loan_int_rate`: Filled with median grouped by `loan_grade`
   - `person_emp_length`: Filled with median grouped by age groups

2. **Categorical Variable Encoding**
   - `person_home_ownership` (RENT, OWN, MORTGAGE, OTHER): One-hot encoding
   - `loan_intent` (6 categories): One-hot encoding
   - `loan_grade` (A-G): Ordinal encoding (A=1, B=2, ..., G=7)
   - `cb_person_default_on_file` (Y/N): Binary encoding

3. **Feature Selection**
   - Mutual Information-based feature selection
   - Selects top features with MI > 0.01 or top 20 features

4. **Data Scaling**
   - StandardScaler normalization for numerical features

#### Machine Learning Models
- **Logistic Regression**: With class weight balancing for imbalanced data
- **Random Forest**: 300 estimators, handles class imbalance
- **XGBoost**: Gradient boosting with automatic class weight adjustment

---

## Project 2: Credit Scoring Model (`scoring/`)

### Overview
Implements a traditional credit scoring model using Weight of Evidence (WoE) transformation and logistic regression. This approach follows industry-standard credit risk modeling practices for regulatory compliance and interpretability.

### Methods Used

#### Weight of Evidence (WoE) Transformation

**Step 1: Fine Classification**
- Splits numerical variables into 20 bins using quantiles
- Calculates WoE for each bin: `WoE = ln(Good_Pct / Bad_Pct)`
- Computes Information Value (IV) to assess predictive power

**Step 2: Coarse Classification**
- Consolidates bins to ensure **monotonicity** (max 5 bins)
- Combines adjacent bins with similar WoE values
- Ensures interpretable and regulatory-compliant patterns

#### Model Building
- **Logistic Regression on WoE Variables**: Interpretable coefficients
- **Scorecard Construction**: Industry-standard credit scoring formulas
  - Score formula: `Score_i = (βi × WoE_i + α/n) × Factor + Offset/n`
  - Parameters: PDO=20, Target Score=600, Target Odds=50:1

#### Population Stability Index (PSI) Analysis
- Compares distribution stability between training and test sets
- Identifies data drift (PSI thresholds: <0.1 stable, 0.1-0.25 moderate, ≥0.25 significant)

#### Class Imbalance Handling
Tests multiple methods and selects best:
- Random Over-Sampling
- SMOTE (Synthetic Minority Over-sampling)
- ADASYN
- Random Under-Sampling
- SMOTE + Tomek Links
- Class Weight Balancing

---

## Differences Between Approaches

| Aspect | Credit Risk (ML Approach) | Scoring (Traditional) |
|--------|---------------------------|----------------------|
| **Methodology** | Standard ML workflow | WoE transformation + Logistic Regression |
| **Interpretability** | Lower | High (monotonic bins, scorecard) |
| **Regulatory Compliance** | May not meet requirements | Industry-standard, compliant |
| **Performance** | Potentially better | Good, interpretable |
| **Feature Engineering** | Flexible | Structured (WoE bins) |
| **Output** | Probabilities | Credit scores + probabilities |
| **Use Case** | Internal risk assessment | Regulatory, business decision-making |


