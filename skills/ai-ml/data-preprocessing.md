---
description: Clean and preprocess datasets with missing values, outliers, feature scaling, encoding, tokenization, and splitting
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in data preprocessing for machine learning. When cleaning and preprocessing datasets, follow these steps:

1. **Explore the data first**:
   - Load with `pandas` and run `df.info()`, `df.describe()`, `df.head()`, `df.shape`.
   - Check data types: identify columns that should be numeric but are stored as strings.
   - Compute null percentages per column: `df.isnull().sum() / len(df) * 100`.
   - Visualize distributions with histograms and box plots for numerics, value counts for categoricals.
   - Identify the target variable and confirm its distribution (check for class imbalance).

2. **Handle missing values**:
   - **Drop**: Remove rows if <5% are missing and missingness is random. Remove columns if >50% missing and not critical.
   - **Impute numerics**: Mean (normal distribution), median (skewed distribution), or KNN imputer for multivariate relationships.
   - **Impute categoricals**: Mode, or create a new "Unknown" category.
   - **Flag missingness**: Add binary indicator columns (`feature_is_missing`) when missingness itself may be informative.
   - Always fit imputers on training data only — use `sklearn.impute.SimpleImputer` or `KNNImputer` in a pipeline.

3. **Detect and handle outliers**:
   - **Statistical**: Flag values beyond 3 standard deviations or 1.5x IQR from Q1/Q3.
   - **Domain-based**: Apply business rules (e.g., age cannot be negative or >150).
   - **Isolation Forest**: For multivariate outlier detection on high-dimensional data.
   - Handling options: cap/clip to bounds (winsorize), transform (log, sqrt), remove, or keep with a flag.
   - Document every outlier decision — removal requires justification.

4. **Feature scaling**:
   - **StandardScaler**: Zero mean, unit variance. Use for algorithms assuming Gaussian inputs (SVM, logistic regression, neural networks).
   - **MinMaxScaler**: Scale to [0, 1]. Use for algorithms sensitive to magnitude (KNN, neural networks with sigmoid).
   - **RobustScaler**: Uses median and IQR. Robust to outliers.
   - **No scaling needed** for tree-based models (Random Forest, XGBoost, LightGBM).
   - Fit the scaler on training data only, then transform train/val/test sets.

5. **Encode categorical variables**:
   - **One-hot encoding**: `pd.get_dummies()` or `OneHotEncoder` for nominal categoricals with <15 unique values.
   - **Ordinal encoding**: For ordered categories (low/medium/high, education levels).
   - **Target encoding**: For high-cardinality categoricals (zip codes, product IDs). Use `category_encoders.TargetEncoder` with cross-validation to avoid leakage.
   - **Label encoding**: Only for tree-based models that can handle arbitrary integer mappings.
   - Handle unseen categories at inference time: use `handle_unknown='ignore'` in `OneHotEncoder`.

6. **Text tokenization** (NLP tasks):
   - Clean text: lowercase, remove HTML tags, normalize unicode, handle contractions.
   - Tokenize with the model-appropriate tokenizer (HuggingFace `AutoTokenizer`, `tiktoken` for OpenAI, `nltk` for classical NLP).
   - Pad or truncate sequences to a fixed length. Set `max_length` based on your data's distribution (e.g., 95th percentile).
   - Create attention masks for transformer models.
   - For classical ML: use `TfidfVectorizer` or `CountVectorizer` with appropriate `max_features`, `ngram_range`, and `min_df`/`max_df`.

7. **Image augmentation** (computer vision tasks):
   - Training augmentations: random horizontal flip, rotation (10-15 degrees), color jitter, random crop, cutout/random erasing.
   - Validation/test: only resize and normalize — no random augmentations.
   - Use `torchvision.transforms` or `albumentations` (more flexible and faster).
   - Normalize with dataset-specific or ImageNet means and standard deviations.
   - Resize to model's expected input size (224x224, 299x299, etc.).

8. **Train/test splitting**:
   - Use `train_test_split` with `stratify=y` for classification tasks.
   - For time series: split chronologically — never shuffle. Use `TimeSeriesSplit` for cross-validation.
   - For grouped data (e.g., multiple samples per patient): use `GroupShuffleSplit` to prevent data leakage.
   - Typical split: 80/10/10 or 70/15/15 for train/validation/test.
   - Create the split once and save the indices for reproducibility.

Always wrap preprocessing in `sklearn.pipeline.Pipeline` or a custom pipeline class to ensure consistent application to new data.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
