# 🚀 Predicting E-commerce Customer Churn with Smart AI

In today’s competitive e-commerce landscape, understanding **why customers stop engaging** is more critical than ever. For the **Terno Internship Challenge**, my goal was to build a compact yet intelligent model capable of identifying customers most at risk of churning — using only a small and noisy dataset.

---

## 🧩 The Challenge

The dataset simulated a typical e-commerce environment: a handful of behavioral features such as:

* `VisitsLast30Days`
* `TimeOnSite`
* `PurchaseCount`
* `HasSupportTicket`

The twist?
The data was *tiny* — only a few dozen rows — making it a test of precision and creativity rather than raw computation.
This wasn’t about “deep learning.” It was about **smart learning**.

---

## ⚙️ The Approach

I structured the project using a **clean machine learning pipeline**:

1. **Exploration & Cleaning** — checked variance, nulls, and distribution balance.
2. **Feature Scaling** — standardization for fair model training.
3. **SMOTE & Class Weights** — tackled class imbalance elegantly.
4. **Model Experiments** — tested Logistic Regression, RandomForest, and LightGBM.
5. **Evaluation** — through 5-fold Stratified CV and ROC-AUC scoring.

After experimentation, a **class-weighted RandomForest** emerged as the most stable model, giving:

* **ROC-AUC ≈ 0.69**
* **Accuracy ≈ 60–70% (depending on threshold)**
* **Robust interpretability via SHAP and permutation importance**

---

## 🔍 Explainability Matters

Small data means every decision counts.
Using **SHAP values**, I visualized how features impacted predictions:

* 🕒 `TimeOnSite` had the **strongest influence** on churn risk.
* 💬 `HasSupportTicket` and `VisitsLast30Days` were secondary but insightful.
* 🛒 `PurchaseCount` had minimal predictive power — customers bought less but didn’t necessarily churn.

This transparency ensures that stakeholders can **trust the model**, not just its output.

---

## 🎯 Key Learnings

* With small data, **robust validation** is more important than model complexity.
* **Explainability** should always accompany performance metrics.
* Even simple models can yield strategic insights when properly tuned.

---

## 🌟 The Outcome

A ready-to-deploy notebook and pipeline that:

* Detects churn-prone users
* Generates human-interpretable insights
* Is lightweight and production-friendly

This challenge was a perfect blend of data science fundamentals, model interpretability, and storytelling — proving that **impactful AI isn’t about size, but about clarity.**

---

📘 *Project Repository:* [Terno Internship Challenge on GitHub](https://github.com/anshika1234-python/Terno_internship_challenge)
