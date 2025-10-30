# Terno_internship_challenge
# E-commerce Churn Prediction — Terno Internship Challenge

**Author:** *Your Name*
**Project:** Terno Internship — Churn Prediction Case Study
**Repository:** `E-commerce_churn_prediction`
**Date:** *(fill in)*

---

## 1. Project Overview

This project implements an end-to-end churn prediction pipeline for an e-commerce dataset as part of the Terno Internship challenge. The goal is to predict whether a user will churn using behavioral features (visits, time on site, purchases, support tickets) and produce a reproducible, explainable model suitable for evaluation.

---

## 2. Files & Structure

```
E-commerce_churn_prediction/
├─ data/
│  └─ ecommerce_churn.xlsx
├─ notebooks/
│  └─ ecommerce_churn_project.ipynb   <-- main notebook
├─ models/
│  ├─ small_data_rf_pipeline.joblib
│  ├─ final_submission_pipeline.joblib
│  ├─ perm_importance_final.csv
│  ├─ shap_mean_abs_final.csv
│  └─ *.png (plots)
├─ README.md
└─ requirements.txt
```

---

## 3. Challenge Summary (from Terno PDF)

* Build a reproducible Jupyter notebook demonstrating:

  * Problem understanding, EDA, preprocessing
  * Model training, hyperparameter tuning, evaluation
  * Explainability (feature importance & SHAP)
  * A final reproducible pipeline and short write-up

This repo follows those exact deliverables.

---

## 4. Data Description

The dataset contains behavioral user features (example):

* `UserID` — unique user identifier
* `VisitsLast30Days` — number of website visits in the last 30 days
* `TimeOnSite` — average time spent on site per visit (minutes)
* `PurchaseCount` — number of purchases
* `HasSupportTicket` — whether a support ticket exists (Yes/No)
* `Churn` — target (Yes/No)

*Note:* dataset is intentionally small for the challenge (approx. 50 rows). This affects model stability and evaluation noise.

---

## 5. Key Steps & Decisions (what I did)

1. **Data loading & sanity checks**

   * Ensured correct paths and installed `openpyxl`.
   * Verified OneDrive file availability; used `../data` relative path.

2. **Exploratory Data Analysis**

   * Basic distributions, class balance checks, and correlation plots.

3. **Preprocessing**

   * Converted categorical `HasSupportTicket` to binary (0/1).
   * Standard scaled numeric features within pipelines for reproducibility.
   * Dropped zero-variance features (none in this dataset).

4. **Baseline models**

   * Logistic Regression (baseline) and Random Forest baseline.
   * Initial imbalance handling: class weights and SMOTE were compared.

5. **Model selection**

   * Compared approaches via Stratified K-Fold CV:

     * `class_weight='balanced'` RandomForest performed best on CV.
     * SMOTE was tested but CV suggested class-weighted RF was more stable.
   * Compact `GridSearchCV` tuned RF hyperparameters.

6. **Small-data optimization**

   * Recognized dataset size limits; used compact models and robust CV.
   * Tuned classification threshold (not only 0.5) to optimize F1 for business preference.

7. **Explainability**

   * Permutation importance (model-agnostic).
   * SHAP (TreeExplainer) to explain feature influence and per-sample impacts.

---

## 6. Problems Faced & How I Solved Them

* **Excel file opened as binary in VS Code** — solution: read via `pd.read_excel()` and avoid editing `.xlsx` as text.
* **Missing `openpyxl`** — installed via `pip install openpyxl`.
* **SHAP API differences** — `shap.Explainer` sometimes failed additivity checks; implemented robust fallback to `TreeExplainer` and normalized outputs for plotting.
* **LightGBM warnings** — LightGBM initially reported zero usable features (due to data shape / small sample); switched to class-weighted RF for stability.
* **Extremely small dataset** — addressed by emphasizing cross-validation mean/std, using class weights and conservative grids, and interpreting SHAP/permutation importances rather than relying only on single test metrics.

---

## 7. Results (final)

* **Final model:** RandomForest (class_weight='balanced'), tuned via GridSearchCV.
* **Final threshold:** 0.26 (chosen to maximize F1 for the dataset)
* **Final test performance (example)**:

  * Accuracy: `0.400`
  * Precision: `0.400`
  * Recall: `1.000`
  * F1-score: `0.571`
  * ROC-AUC: `~0.70` (use CV mean/std for stability)
* **Top features (consistent across methods):**

  * `TimeOnSite`, `VisitsLast30Days`, `HasSupportTicket`, `PurchaseCount`

> Note: metrics are noisy because of the small dataset. Prefer CV mean/std and SHAP/permutation evidence for conclusions.

---

## 8. How to run (reproduce)

1. Create a Python environment (recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # Linux/Mac
   .venv\Scripts\activate      # Windows
   pip install -r requirements.txt
   ```

2. Open notebook:

   ```bash
   jupyter lab
   # then open notebooks/ecommerce_churn_project.ipynb
   ```

3. Run top-to-bottom. If packages like `shap`, `xgboost`, or `lightgbm` are missing, install them as needed:

   ```bash
   pip install shap xgboost lightgbm
   ```

---

## 9. What I would do with more time / data (next steps)

* Collect more labeled data to stabilize training and CV.
* Add richer features (recency of last purchase, total revenue, session paths).
* Run nested CV and stacking ensembles (RF + XGBoost + LR meta) once more data available.
* Calibrate probabilities (e.g., `CalibratedClassifierCV`) for production.
* Design an A/B test to measure whether intervention based on model predictions reduces churn.

---

## 10. Submission notes

* The notebook `notebooks/ecommerce_churn_project.ipynb` is the canonical submission.
* All final artifacts (trained pipeline, SHAP CSV, PNGs, `final_report.md`) are saved in `models/`.
* Add a Colab badge or Codespaces instructions to make it easier for reviewers to run.

---

## 11. Contact

* If you want any changes (e.g., convert final report to PDF, include Dockerfile, or add an API demo), I can add those quickly.

---

**Thank you — good luck with the Terno Internship submission!**
If you want, I can also:

* Create a single zipped submission artifact ready to upload, or
* Automatically push this repo to GitHub with a polished GitHub Actions workflow that executes the notebook.
