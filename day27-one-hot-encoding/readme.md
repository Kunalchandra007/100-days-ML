# Day 27 - One-Hot Encoding

## Resources
Video Link : https://youtu.be/U5oCv3JKWKA

---

## Notebook: day27.ipynb

### Lesson Overview
Convert unordered categorical variables to binary feature columns.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import numpy as np, pandas as pd`
- `from sklearn.preprocessing import OneHotEncoder`

**Cell 2: Load data**
- `df = pd.read_csv('cars.csv')`

**Cell 3-4: Explore data**
- `df.head()` - Preview car data
- `df['owner'].value_counts()` - See owner categories

**Cell 5: Pandas get_dummies (Method 1)**
- `pd.get_dummies(df, columns=['fuel','owner'])`
- Simple one-hot encoding without preprocessing
- Creates binary columns for each category

**Cell 6: K-1 Encoding (Drop First)**
- `pd.get_dummies(df, columns=['fuel','owner'], drop_first=True)`
- Remove one category per feature to prevent multicollinearity
- K categories → K-1 binary features

**Cell 7: Sklearn OneHotEncoder (Method 2)**
- `ohe = OneHotEncoder(drop='first', sparse=False, dtype=np.int32)`
- `drop='first'` - K-1 encoding
- `sparse=False` - Dense array (vs sparse matrix)
- `dtype=np.int32` - Output type

**Cell 8: Train-test split**
- Split features and target

**Cell 9: Preview training features**
- `X_train.head()` - Show original features

**Cell 10: Fit OneHotEncoder**
- Learn categories from training set

**Cell 11-12: Transform both sets**
- `X_train_new = ohe.fit_transform(X_train[['fuel','owner']])`
- `X_test_new = ohe.transform(X_test[['fuel','owner']])`
- **Critical:** Fit only on train, transform both sets

**Cell 13: Check dimensions**
- `X_train_new.shape` - Verify binary features created

**Cell 14: Stack with numeric features**
- Combine one-hot features with numeric features
- Create complete feature matrix for modeling

**Cell 15: Top categories only**
- Find number of unique brands

**Cell 16: Define frequency threshold**
- Find brands appearing below threshold (rare)

**Cell 17: Group rare categories**
- Replace low-frequency brands with 'uncommon' label
- Reduces number of features

**Cell 18: One-hot with grouped categories**
- Now manageable number of features

### How One-Hot Encoding Works:
- Category A: [1, 0, 0]
- Category B: [0, 1, 0]
- Category C: [0, 0, 1] (or [0, 0] in K-1)
- Binary representation with no ordinal assumption

### Key Methods:
- `pd.get_dummies()` - Simple pandas encoding
- `OneHotEncoder()` - Sklearn for pipelines
- `drop='first'` - K-1 encoding to prevent multicollinearity
- `sparse=False` - Dense output for compatibility

### When to Use:
- Unordered categories (no natural ranking)
- When category order doesn't matter
- Linear models (must use one-hot)
- Tree models (acceptable)

### When NOT to use:
- When categories have natural order (use ordinal encoding)
- Too many rare categories (group them first)
- Extreme dimensionality issues (select top categories)

### Important Concepts:
- K-1 encoding prevents perfect multicollinearity
- High cardinality (many categories) creates many features
- Group rare categories to reduce dimensionality
- Last category represented as all zeros in K-1 encoding
- One-hot is standard for linear models
