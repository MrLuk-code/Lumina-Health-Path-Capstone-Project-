# Lumina-Health-Path-Capstone-Project-
# Lumina HealthPath Capstone: Automated Diagnostic Risk Classification

An automated, clinically validated machine learning pipeline designed to replace manual, threshold-based health screenings with an interpretable risk-sensitive classification model.

## 📌 Project Overview
Lumina HealthPath is a Series B scale-up specializing in non-invasive health insights powered by wearable and longitudinal data. As the volume of incoming patient files scales up by 500% next quarter, the current approach—relying on fragmented Excel macros and hard-coded "if-else" thresholds—presents a major operational bottleneck. 

This project delivers a statistically grounded, interpretable **Binary Classification Model** using **Logistic Regression** to screen 50,000 anonymized patient records and separate them accurately into `Stable` or `High Risk` cohorts.

### 📉 Business Case & Operational Impact
* **Financial Deficit if Unsolved:** Failure to automate this manual review process introduces a projected **$1.2M annual operational deficit** driven by soaring clinical staffing requirements.
* **Target Objective:** Safely automate **90% of initial patient screenings** while maintaining a strict safety net to minimize missed critical diagnoses.

---

## ⚙️ Core Constraints & Guardrails
To satisfy compliance frameworks and ensure clinical safety, the implementation adheres strictly to the following parameters:
* **Algorithm Constraints:** Must utilize an interpretable linear architecture (**Logistic Regression**) so that medical auditors can transparently track metabolic hazard weights.
* **Primary Optimization Metric:** Must achieve a **Recall score of ≥ 0.85** on the validation test set to minimize critical False Negatives.
* **Data Splitting Order:** To eliminate data leakage, the data split *must* be fully executed prior to any data transformations or scaling routines.
* **Isolation of Scaling:** Feature scaling (e.g., `StandardScaler`) must be isolated strictly to independent structural vectors ($X$) and **never** applied to the target classification vector ($y$).

---

## 🛠️ Pipeline Architecture & Implementation Phases

### Phase 1: Data Engineering & Exploratory Analysis
* **Objective:** Audit patient data quality and establish a clean, standardized foundation for predictive modeling.
* **Key Tasks:** Map multivariable feature correlations, manage missing metabolic indices using robust median imputation, and split/scale variables appropriately.
* **Artifacts:** Jupyter Notebook featuring correlation heatmaps, Descriptive Statistics Summary, and Data Imputation Strategy documentation.

### Phase 2: Model Development & Parameter Tuning
* **Objective:** Construct a stable baseline Logistic Regression framework and balance weights to address minority-class sensitivity.
* **Key Tasks:** Initialize the model utilizing `class_weight='balanced'`, analyze weight distributions, and log regularization penalties ($C$-values).
* **Artifacts:** Trained Logistic Regression model object and Model Coefficient Report (Interpretable Log-Odds).

### Phase 3: Clinical Validation & Evaluation
* **Objective:** Rigorously validate model boundaries against performance constraints and establish the optimal adjusted classification threshold.
* **Key Tasks:** Map Precision-Recall curves, visualize model performance using a dedicated Confusion Matrix, and adjust the decision threshold to guarantee the minimum Recall target.
* **Artifacts:** Final Model Performance Report (Recall, F1-Score, Accuracy) and Threshold Adjustment Recommendations.

---

## 📊 Performance Rubric & Common Pitfalls

| Evaluation Criteria | Priority Level | What Success Looks Like | Critical Pitfalls to Avoid |
| :--- | :--- | :--- | :--- |
| **01 Preprocessing & Scaling** | 🔴 Critical | Data split occurs first. Scaling parameters are learned *only* from the training subset. | Scaling the entire dataset simultaneously; scaling the target label ($y$). |
| **02 Performance Optimization** | 🔴 Critical | Recall score consistently evaluates at $\ge 0.85$ via strategic threshold tuning. | Prioritizing general Accuracy while overlooking high False Negative rates. |
| **03 Interpretability Analysis** | 🟡 Important | Model weights are mapped back to original feature names for clinical verification. | Confusing predictive correlation with true medical causation in stakeholder presentations. |
| **04 Visualization & Reports** | 🟡 Important | Technical plots (Confusion Matrices, PR Curves) are clearly labeled and scannable. | Using overly dense engineering jargon in summaries meant for clinical auditors. |

---

## 🚀 Getting Started

### Prerequisites
Ensure your local Python environment includes the following data science libraries:
```bash
pip install numpy pandas scikit-learn notebook matplotlib seaborn
