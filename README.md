# 🧠 Terno Internship Challenge – E-commerce Churn Prediction

## 📋 Project Overview

This repository contains my submission for the **Terno Internship Challenge**, focused on predicting **e-commerce customer churn** from a small behavioral dataset.
The goal was to design a **robust, interpretable, and efficient machine learning model** capable of detecting at-risk customers while explaining *why* those predictions were made.

---

## 🗂️ Repository Structure

```
Terno_internship_challenge/
│
├── notebooks/
│   └── ecommerce_churn_project.ipynb      # Full model development notebook
│
├── data/
│   └── ecommerce_churn.xlsx               # Source dataset
│
├── models/
│   ├── shap_global_bar.png                # Global feature importance
│   ├── shap_beeswarm.png                  # Per-sample SHAP visualization
│   ├── shap_mean_abs_importance.csv       # Numeric SHAP summary
│   └── small_data_rf_pipeline.joblib      # Final trained RandomForest model
│
├── blog_draft.md                          # Story-style project blog
├── README.md                              # This documentation
└── requirements.txt                       # Dependencies
```

---

## ⚙️ Methodology

### 1️⃣ Data Preparation

* Inspected variance, nulls, and categorical structure.
* Detected and handled imbalance via **SMOTE** and **class weights**.
* Applied **StandardScaler** for normalization.

### 2️⃣ Modeling

Tested multiple algorithms:

| Model                    | ROC-AUC (CV) | Notes                               |
| ------------------------ | ------------ | ----------------------------------- |
| Logistic Regression      | ~0.54        | Poor recall on minority class       |
| Random Forest (weighted) | **~0.69**    | Most stable and interpretable       |
| LightGBM                 | 0.50         | Overfit due to low feature variance |

Final model: **RandomForestClassifier (class_weight='balanced')**

---

## 📊 Evaluation Results

| Metric    | Default Threshold (0.5) | Best Threshold (0.26) |
| --------- | ----------------------- | --------------------- |
| Accuracy  | 0.50                    | 0.70                  |
| Precision | 0.57                    | 0.80                  |
| Recall    | 0.67                    | 0.75                  |
| F1-Score  | 0.62                    | **0.80**              |
| ROC-AUC   | **0.688**               | -                     |

**Top Features (SHAP + Permutation Importance):**

1. `TimeOnSite` – key engagement driver
2. `VisitsLast30Days` – consistency indicator
3. `HasSupportTicket` – signals dissatisfaction
4. `PurchaseCount` – less predictive but complementary

---

## 🧩 Explainability

The project integrated **SHAP interpretability**:

* `shap_global_bar.png` shows average feature influence.
* `shap_beeswarm.png` visualizes individual customer impacts.
* All SHAP results exported to CSV for reproducibility.

---

## 🧪 Key Challenges & Improvements

| Phase              | Challenge               | Resolution                                     |
| ------------------ | ----------------------- | ---------------------------------------------- |
| Small dataset      | Overfitting risk        | Used cross-validation + balanced weights       |
| Class imbalance    | Poor recall on churners | Added SMOTE + class weighting                  |
| Model transparency | Black-box problem       | Added SHAP + permutation interpretation        |
| Performance tuning | Low AUC variance        | Performed grid search over limited param space |

---

## 🏁 Final Outcome

* ✅ Compact, interpretable, production-ready RandomForest pipeline
* ✅ Explainable ML artifacts (SHAP + permutation)
* ✅ 5-fold CV stability reporting
* ✅ Full GitHub documentation and reproducibility

---

## 🚀 How to Run

```bash
# Clone the repo
git clone https://github.com/anshika1234-python/Terno_internship_challenge.git
cd Terno_internship_challenge

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook notebooks/ecommerce_churn_project.ipynb
```

---

## 📚 Author

**Anshika Aggarwal**
🎓 MSc Physics (Electronics) | Data Science & AI Trainee
💡 Interested in Machine Learning, Explainable AI, and Applied Analytics
📬 [GitHub](https://github.com/anshika1234-python)

---

## 📘 Reference

This project was developed as part of the **Terno Internship Challenge** to demonstrate applied data science, interpretability, and reproducible ML pipeline design.
