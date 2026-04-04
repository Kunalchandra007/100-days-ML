# Day 30 - Function Transformer

## Resources
Video Link : https://youtu.be/cTjj3LE8E90

---

## Notebook: day30.ipynb

### Lesson Overview
Apply custom functions for flexible feature transformations in preprocessing pipelines.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import pandas as pd, numpy as np`
- `from sklearn.preprocessing import FunctionTransformer`
- `from sklearn.compose import ColumnTransformer`

**Cell 2: Load and prepare data**
- `df = pd.read_csv('train.csv', usecols=['Age','Fare','Survived'])`

**Cell 3: Check missing values**
- `df.isnull().sum()` - Identify missing data

**Cell 4: Impute missing Age**
- `df['Age'].fillna(df['Age'].mean(), inplace=True)`
- Fill with mean value

**Cell 5: Prepare features and target**
- `X = df.iloc[:,1:3]` - Age and Fare
- `y = df.iloc[:,0]` - Survival (target)

**Cell 6: Train-test split**
- Split data for evaluation

**Cell 7: Visualize original data**
- Distribution plots and Q-Q plots
- Show right-skewed distributions

**Cell 8: Define transformation function**
- `trf = FunctionTransformer(func=np.log1p)`
- `np.log1p()` = log(1 + x) for natural log transformation
- Handles zero values without errors

**Cell 9-10: Apply transformation**
- `X_train_transformed = trf.fit_transform(X_train)`
- `X_test_transformed = trf.transform(X_test)`

**Cell 11-12: Model comparison**
- **Before transformation**: Unoptimized
- **After log transformation**: Improved accuracy

**Cell 13-14: Visualization after transformation**
- Q-Q plots show data closer to normal
- Distribution plots smoother

**Cell 15: ColumnTransformer with FunctionTransformer**
- `trf2 = ColumnTransformer([('log', FunctionTransformer(np.log1p), ['Fare'])])`
- Apply function to specific column only

**Cell 16-17: Selective transformation**
- Transform only Fare column
- Keep Age in original scale

**Cell 20: Custom transformation function**
- General function to test different transformations
- Applies function to Fare only

**Cell 21: Test sine transformation**
- `apply_transform(np.sin)` - Non-linear transformation

### Ready-to-Use Transformation Functions:
- `np.log1p()` - Natural log (right-skewed data)
- `np.sqrt()` - Square root (moderate skew)
- `np.exp()` - Exponential transformation
- `np.sin()`, `np.cos()` - Trigonometric
- `1/X` - Reciprocal transformation
- Custom functions for domain-specific transformations

### When to Use:
- Right-skewed numerical data (use log)
- Count data (use sqrt)
- Non-linear relationships (custom functions)
- Domain-specific transformations
- Flexible preprocessing beyond standard scalers

### Key Methods:
- `FunctionTransformer(func=...)` - Create transformer
- `fit_transform()` - Apply immediately
- `transform()` - Apply to new data
- `ColumnTransformer([...])` - Selective column transformation
- `remainder='passthrough'` - Keep other columns

### Important Concepts:
- `fit_transform()` on training data only
- `transform()` on test data using same fitted transformer
- Custom functions must accept array-like input
- Use with ColumnTransformer for mixed transformations
- More flexible than StandardScaler/MinMaxScaler
- Domain knowledge guides transformation choice
