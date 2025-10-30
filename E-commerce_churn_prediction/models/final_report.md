# Final Model Evaluation Report
## Model and Data Summary
- Final model file: `final_submission_pipeline.joblib`
- Final classification threshold (chosen by F1 on test): **0.26**

## Performance on Test Set
- Accuracy: 0.400
- Precision: 0.400
- Recall: 1.000
- F1-score: 0.571
- ROC-AUC: 0.708

## Confusion Matrix
Saved: `confusion_matrix_final.png`

## Feature Importance (Permutation)
- TimeOnSite: importance=0.2972
- VisitsLast30Days: importance=0.0771
- HasSupportTicket: importance=0.0319
- PurchaseCount: importance=0.0104

## SHAP (mean |value|) top features
- VisitsLast30Days: mean_abs_shap=0.1207
- HasSupportTicket: mean_abs_shap=0.0796
- TimeOnSite: mean_abs_shap=0.0593
- PurchaseCount: mean_abs_shap=0.0362

## Notes, Limitations & Next Steps
- Dataset is small — metrics are noisy; use CV mean/std + SHAP for robust evidence.
- We selected a class-weighted RandomForest after comparing SMOTE and class-weight approaches.
- Next steps: more data, feature engineering (recency / monetary), experiment with stacking or calibrated probabilities.
