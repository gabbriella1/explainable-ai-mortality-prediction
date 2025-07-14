# Explainable AI for Medical Time-Series Data

## Overview

This project explores the use of explainable machine learning models to predict in-hospital mortality based on anonymized laboratory time-series data. By leveraging tree-based classifiers and interpretability tools, we aim to create transparent decision-support systems for clinicians that are both accurate and trustworthy.

---

## Motivation

Modern hospitals record vast amounts of time-stamped clinical data—much of it underused. By applying machine learning to these data streams, we can identify early warning signals of deterioration before traditional alarms would activate.

However, black-box models are hard to trust. Doctors and regulators require transparency, especially in life-critical applications. That’s why we integrate explainable AI techniques to reveal how the models arrive at their predictions.

---

## Objectives

- **Predictive Performance**: Train and compare four tree-based models on hospital time-series features.
- **Explainability**: Use global and local XAI techniques to interpret the best-performing model.
- **Clinical Relevance**: Identify key biochemical predictors and ensure explanations are understandable to medical professionals.

---

## Data

- **Source**: Two anonymized Excel files (375 train + 110 test records)
- **Content**: Time-stamped lab tests aggregated by patient
- **Preprocessing**:
  - Aggregated lab values with mean, min, max, and last observed
  - Added stay duration as a feature
  - Median imputation for missing values
  - Used only features present in both sets to ensure alignment

---

## Methodology

### Models Trained
- Random Forest  
- XGBoost  
- HistGradientBoosting  
- **LightGBM** (selected for best generalization)

### Evaluation Metrics
- Precision, Recall, F1 Score, Accuracy
- Separate results for minority (class 1) and majority (class 0) classes
- Custom decision threshold (0.6) to reduce false negatives

### Explainability Techniques
- **Global**: Feature importance, Permutation Importance, SHAP values
- **Local**: SHAP force plots, LIME for individual patient explanations
- **Continuity Testing**: Verified explanation stability using CO-12 metric (ΔSHAP ≈ 0.0015)

---

## Results

### Predictive Performance (Class 1 - minority class)

| Model                  | Precision | Recall | F1 Score | Accuracy |
|-----------------------|-----------|--------|----------|----------|
| Random Forest          | 0.85      | 0.85   | 0.85     | 0.96     |
| XGBoost                | 0.86      | 0.92   | 0.89     | 0.97     |
| HistGradientBoosting   | 0.86      | 0.92   | 0.89     | 0.97     |
| **LightGBM**           | 0.83      | 0.77   | 0.80     | 0.95     |

LightGBM was chosen due to its better generalization and interpretability.

### Key Features Identified
- **Lactate Dehydrogenase (last value)**
- **Hypersensitive C-Reactive Protein (min and last)**
- **Lymphocyte Percentage** (mean, min, max, last)
- **Stay Duration**

---

## Insights & Explanations

- SHAP showed consistent feature impact across the dataset
- LIME confirmed key features in local predictions
- Explanations are robust to minor input changes (continuity test passed)

> These tools make it easier for clinicians to understand and trust the model’s decisions.

---

## Clinical Relevance

- Helps predict mortality risk earlier than traditional methods
- Supports clinical decisions around escalation or discharge
- Transparent enough to meet **GDPR** and **EU AI Act** requirements

---

## Future Work
- Expand to multi-center datasets for generalizability
- Conduct fairness audits and add uncertainty quantification

---

## References

Key references include Lundberg et al. (SHAP), Ribeiro et al. (LIME), and recent studies on interpretable healthcare AI.

(See full list in the original report)

---

## Conclusion

This project demonstrates that interpretable machine learning models—particularly LightGBM—can predict patient outcomes with high accuracy while providing actionable, transparent insights. With further tuning and testing, models like this can be integrated into real-world clinical workflows.

