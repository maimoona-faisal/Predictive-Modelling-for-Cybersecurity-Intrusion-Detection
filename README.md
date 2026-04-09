# Predictive-Modelling-for-Cybersecurity-Intrusion-Detection

A supervised machine learning project focused on binary classification of network intrusion events using session-level traffic data, built and evaluated in **SAS Model Studio**.

---

## Overview

This project applies predictive modelling techniques to detect cybersecurity intrusions from network session data. Two models were developed, tuned, and evaluated — **Gradient Boosting** and **Random Forest** — with Random Forest selected as the project champion based on validation performance.

The work was completed as part of a **Data Mining and Predictive Modelling** module, following the CRISP-DM methodology.

---

## Dataset

| Property | Details |
|---|---|
| Source | [Kaggle — Cybersecurity Intrusion Detection Dataset](https://www.kaggle.com/datasets/dnkumars/cybersecurity-intrusion-detection-dataset) |
| License | MIT |
| Observations | 9,537 rows |
| Variables | 11 columns (10 predictors + 1 target) |
| Target | `attack_detected` → 0 = No attack, 1 = Attack detected |

---

## Models

### Gradient Boosting
- 400 trees, learning rate 0.03, subsample rate 0.8
- L2 regularization = 3, early stopping on log loss
- Validation Accuracy: **0.8741** | Validation AUC: **0.8794**

### Random Forest ⭐ Champion
- 300 trees, probability voting, Gini splitting criterion
- Max depth 8, 5 variables per split, bag sample proportion 0.8
- Validation Accuracy: **0.8749** | Validation AUC: **0.8794**

Random Forest was selected as the final champion for achieving the highest validation accuracy with a smaller train-validate gap (0.63 percentage points), indicating better generalisation to unseen data.

---

## Key Findings

The most predictive variables across both models were:

1. `failed_logins` — dominant predictor (relative importance = 1.0)
2. `login_attempts` — strong secondary predictor
3. `ip_reputation_score` — meaningful risk signal
4. `browser_type` — moderate contribution
5. `session_duration` / `encryption_used` — low impact

Suspicious authentication behaviour and IP reputation were consistently the strongest signals for intrusion detection.

---

## Repository Structure

```
├── model_deployment/
│   ├── package.json        # SAS Model Studio import package
│   └── request.json        # SAS Model Studio request configuration
├── report/
│   └── Predictive_Modelling_Report.pdf   # Full project report
└── README.md
```

> To use the model deployment files, download both `package.json` and `request.json` and import them into **SAS Model Studio**.

---

## Tools & Environment

- **Platform:** SAS Model Studio
- **Methodology:** CRISP-DM
- **Task Type:** Supervised Binary Classification
- **Data Split:** 70% training (5,970 obs) / 30% validation (2,558 obs), stratified sampling
