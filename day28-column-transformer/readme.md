# Day 28 - Column Transformer

## Resources
Video Link : https://youtu.be/5TVj6iEBR4I

---

## Notebook: day28.ipynb

### Lesson Overview
Apply different preprocessing transformations to different column subsets systematically.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import numpy as np, pandas as pd`
- `from sklearn.impute import SimpleImputer`
- `from sklearn.preprocessing import OneHotEncoder, OrdinalEncoder`
- `from sklearn.compose import ColumnTransformer`

**Cell 2: Load data**
- `df = pd.read_csv('covid_toy.csv')`

**Cell 3: Explore data**
- `df.head()` - Preview mixed data types

**Cell 4: Check missing values**
- `df.isnull().sum()` - Count missing per column

**Cell 5: Train-test split**
- Split into features and target

**Cell 6: View training features**
- `X_train` - Mixed data types (numeric, categorical)

### Manual Approach (Without ColumnTransformer):

**Cell 7: Manual imputation**
- Limited to single column or requires separate handling

**Cell 8: Manual ordinal encoding**
- Apply to cough column

**Cell 9: Manual one-hot encoding**
- Apply to gender and city columns

**Cell 10: Manual concatenation**
- Complex and error-prone

### Efficient Approach (With ColumnTransformer):

**Cell 11: ColumnTransformer**
- `from sklearn.compose import ColumnTransformer`
- Unified preprocessing framework

**Cell 12: Define transformers**
- Create transformer list with multiple transformations
- Each tuple: (name, transformer, column_list)
- `remainder='passthrough'` - Keep other columns unchanged

**Cell 13: Fit and transform training**
- `transformer.fit_transform(X_train)`
- Result shape verified

**Cell 14: Transform test set**
- `transformer.transform(X_test)`
- Apply same transformations to test data

### Advantages of ColumnTransformer:
1. **Clarity**: Define all preprocessing in one place
2. **Consistency**: Fit on train, apply to test automatically
3. **Pipeline compatible**: Integrate with scikit-learn pipelines
4. **Multiple transformations**: Handle mixed data types efficiently
5. **Reproducibility**: Save transformer for production use

### Key Methods:
- `ColumnTransformer()` - Main class
- `fit_transform()` - Fit and transform training data
- `transform()` - Apply to test/new data
- `remainder='passthrough'` - Keep unmapped columns
- `remainder='drop'` - Discard unmapped columns

### Important Concepts:
- Fit ONLY on training data
- Apply same transformer to test/validation/production data
- Prevents data leakage from test set statistics
- Production-ready preprocessing pipeline
- Handles mixed numerical and categorical data elegantly
