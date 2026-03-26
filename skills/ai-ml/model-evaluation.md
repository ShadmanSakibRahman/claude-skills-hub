---
description: Evaluate ML model performance with metrics, cross-validation, learning curves, feature importance, and bias detection
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in machine learning model evaluation. When evaluating model performance, follow these steps:

1. **Select appropriate metrics based on the task**:
   - **Binary classification**: Accuracy (only if balanced), Precision, Recall, F1-score, ROC-AUC, PR-AUC (preferred for imbalanced data), log loss.
   - **Multi-class classification**: Macro/micro/weighted F1, per-class precision/recall, top-k accuracy, confusion matrix.
   - **Regression**: MSE, RMSE, MAE, MAPE, R-squared, adjusted R-squared.
   - **Ranking**: NDCG, MAP, MRR.
   - Choose the primary metric based on business impact: if false negatives are costly (medical diagnosis), optimize recall; if false positives are costly (spam filtering), optimize precision.

2. **Generate the confusion matrix**:
   - Use `sklearn.metrics.confusion_matrix` and `ConfusionMatrixDisplay`.
   - Normalize by row (recall per class) to identify which classes the model struggles with.
   - Analyze off-diagonal entries — which classes are most commonly confused?
   - For multi-class: create both a heatmap and a per-class metrics table.

3. **Compute precision, recall, F1**:
   - Use `classification_report(y_true, y_pred)` for a full summary.
   - Report macro-averaged (equal weight to all classes) and weighted-averaged (weight by class frequency) scores.
   - Plot precision-recall curves per class using `PrecisionRecallDisplay`.
   - Determine the optimal probability threshold — default 0.5 is often not optimal. Use the threshold that maximizes F1 or meets a minimum precision/recall requirement.

4. **ROC-AUC analysis**:
   - Plot the ROC curve using `RocCurveDisplay.from_predictions()`.
   - Report AUC score. AUC > 0.9 is excellent, 0.8-0.9 is good, 0.7-0.8 is fair.
   - For multi-class: use one-vs-rest (OVR) ROC curves.
   - Compare against a random baseline (AUC = 0.5 diagonal line).

5. **Cross-validation**:
   - Use `cross_val_score` with `cv=StratifiedKFold(n_splits=5)` for classification.
   - Report mean and standard deviation of scores across folds.
   - High variance across folds suggests the model is sensitive to the data split.
   - Use `cross_val_predict` to get out-of-fold predictions for the full training set.
   - For time series, use `TimeSeriesSplit` instead of random k-fold.

6. **Learning curves**:
   - Plot training and validation scores vs. training set size using `learning_curve()`.
   - **Overfitting**: Training score is high, validation score is much lower. Fix: more data, regularization, simpler model, dropout.
   - **Underfitting**: Both scores are low. Fix: more features, more complex model, less regularization.
   - **Good fit**: Both scores converge at a high value.
   - Also plot scores vs. training epochs/iterations to check for early stopping opportunities.

7. **Feature importance**:
   - **Tree-based models**: Use `model.feature_importances_` (Gini importance) or permutation importance (`sklearn.inspection.permutation_importance`) which is more reliable.
   - **Linear models**: Use coefficient magnitudes (after feature scaling) for importance.
   - **Model-agnostic**: SHAP values (`shap.TreeExplainer` or `shap.KernelExplainer`) for both global and local explanations.
   - Create a bar chart of top 15-20 features.
   - Identify and remove features with near-zero importance to simplify the model.

8. **Bias detection and fairness**:
   - Define protected attributes (gender, race, age group) and check metrics across subgroups.
   - Compute disparate impact ratio: favorable outcome rate for protected group / rate for reference group. Target > 0.8.
   - Check equalized odds: equal true positive rates and false positive rates across groups.
   - Use `fairlearn.metrics.MetricFrame` to compute metrics per group.
   - If bias is detected: rebalance training data, add fairness constraints, or use post-processing calibration.

9. **Baseline comparison**:
   - Compare against simple baselines: majority class, mean predictor, previous model version, rule-based heuristic.
   - Report the absolute improvement and relative improvement over the baseline.
   - A model that barely beats the baseline may not be worth its complexity.
   - Document all comparison results in a summary table.

Output a comprehensive evaluation report with visualizations, key findings, failure modes, and actionable recommendations.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
