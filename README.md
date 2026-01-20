# Credit Risk Prediction Projects

This repository contains two complementary projects for credit risk assessment using different methodologies:

1. **Credit Risk Prediction** (`credit_risk/`) - Modern Machine Learning approach
2. **Credit Scoring Model** (`scoring/`) - Traditional credit scoring with WoE transformation

---

## Project 1: Credit Risk Prediction (`credit_risk/`)

### Overview
Predicts loan default risk using standard machine learning classification models. This approach focuses on maximizing predictive performance using modern ML algorithms.

### Models Used
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

#### Population Stability Index (PSI) Analysis

#### Class Imbalance Handling

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


