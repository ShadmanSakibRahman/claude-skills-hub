---
description: Create ML pipelines with data loading, preprocessing, training, evaluation, hyperparameter tuning, and serialization
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in building machine learning pipelines. When creating or modifying an ML pipeline, follow these steps:

1. **Set up the project structure**:
   - Organize into `data/`, `notebooks/`, `src/` (with `data/`, `features/`, `models/`, `evaluation/`), `models/` (saved), `configs/`.
   - Use a `requirements.txt` or `pyproject.toml` with pinned versions.
   - Set a random seed globally for reproducibility: `np.random.seed(42)`, `torch.manual_seed(42)`, `random.seed(42)`.

2. **Data loading**:
   - Load data with `pandas` (tabular), `torchvision.datasets` or `tf.data` (images), `datasets` from HuggingFace (NLP).
   - Implement data validation: check for expected columns, dtypes, value ranges, and null percentages.
   - Log dataset statistics: shape, class distribution, feature distributions.
   - Split data early: train (70-80%), validation (10-15%), test (10-15%). Use stratified splitting for imbalanced classes.
   - Never look at or use test data during development — only for final evaluation.

3. **Preprocessing and feature engineering**:
   - Handle missing values: imputation (mean/median/mode), indicator columns, or drop rows.
   - Scale numerical features: `StandardScaler` for Gaussian-like data, `MinMaxScaler` for bounded, `RobustScaler` for outlier-heavy.
   - Encode categoricals: `OneHotEncoder` for low cardinality, `OrdinalEncoder` for ordered, target encoding for high cardinality.
   - Fit preprocessors on training data only, then transform validation/test sets.
   - Use `sklearn.pipeline.Pipeline` or `sklearn.compose.ColumnTransformer` to chain preprocessing steps.

4. **Model training**:
   - **scikit-learn**: Use `Pipeline` with preprocessor and estimator. Call `pipeline.fit(X_train, y_train)`.
   - **PyTorch**: Define `nn.Module`, `DataLoader`, optimizer (`Adam`, lr=1e-3), and loss function. Implement training loop with gradient accumulation if needed. Use `torch.cuda.amp` for mixed precision.
   - **TensorFlow/Keras**: Define `Sequential` or functional model. Compile with optimizer, loss, and metrics. Use `model.fit()` with `callbacks` (EarlyStopping, ModelCheckpoint, ReduceLROnPlateau).
   - Log training metrics per epoch/step using MLflow, Weights & Biases, or TensorBoard.

5. **Evaluation**:
   - Classification: accuracy, precision, recall, F1 (macro/micro/weighted), confusion matrix, ROC-AUC, classification report.
   - Regression: MSE, RMSE, MAE, R-squared, residual plots.
   - Use cross-validation (`cross_val_score` with k=5) on training data for robust estimates.
   - Compare against a baseline: majority class classifier, mean predictor, or previous model version.
   - Plot learning curves to diagnose overfitting vs underfitting.

6. **Hyperparameter tuning**:
   - Define the search space: list parameters and their ranges/options.
   - Use `RandomizedSearchCV` for quick exploration or `Optuna` for Bayesian optimization.
   - Tune on validation set performance, not training performance.
   - Track all experiments with parameters and results.
   - Start with the most impactful hyperparameters (learning rate, regularization, model complexity).

7. **Model serialization and versioning**:
   - **scikit-learn**: `joblib.dump(pipeline, 'model_v1.joblib')`.
   - **PyTorch**: `torch.save(model.state_dict(), 'model_v1.pt')` — save state dict, not the full model.
   - **TensorFlow**: `model.save('model_v1')` (SavedModel format) or `model.save('model_v1.keras')`.
   - Save the preprocessing pipeline alongside the model.
   - Version models with metadata: training date, dataset version, metrics, hyperparameters.
   - Create a `predict.py` script that loads the model and runs inference on new data.

8. **Production readiness**:
   - Write unit tests for data preprocessing and feature engineering functions.
   - Add input validation for inference: check feature types, ranges, and handle missing values.
   - Document model assumptions, limitations, and known failure modes.
   - Create a model card with performance metrics across different data slices.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
