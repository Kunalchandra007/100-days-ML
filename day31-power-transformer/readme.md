# Day 31 - Power Transformer

## Resources
Video Link : https://youtu.be/lV_Z4HbNAx0

---

## Notebook: day31.ipynb

### Lesson Overview
Apply mathematically optimal power transformations (Box-Cox, Yeo-Johnson) to achieve Gaussianity.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `from sklearn.preprocessing import PowerTransformer`
- `from sklearn.linear_model import LinearRegression`
- `from sklearn.model_selection import cross_val_score`

**Cell 2: Load data**
- `df = pd.read_csv('concrete_data.csv')`
- Contains concrete strength prediction features

**Cell 3-5: Explore data**
- `df.head()`, `df.shape`, `df.isnull().sum()`, `df.describe()`

**Cell 6-7: Prepare features and target**
- `X = df.drop(columns=['Strength'])` - Features
- `y = df.iloc[:,-1]` - Target (Strength)

**Cell 8: Train-test split**
- Split for evaluation

**Cell 9: Baseline model performance**
- Model without transformation (~0.61 R²)

**Cell 10: Cross-validation baseline**
- Verify baseline with 10-fold CV

**Cell 11: Distribution analysis before transformation**
- Plot distributions for all features
- Identify skewness and deviation from normality

**Cell 12-13: Box-Cox transformation**
- `pt = PowerTransformer(method='box-cox')`
- `X_train_transformed = pt.fit_transform(X_train + 0.000001)`
- Must add small constant (Box-Cox requires positive values)
- `pt.lambdas_` - Shows learned lambda parameters per feature

**Cell 14-15: Model with Box-Cox**
- Improved R² score (~0.65)
- Better model fit through better feature distributions

**Cell 16-17: Cross-validation with Box-Cox**
- Consistency across folds confirmed

**Cell 18-19: Distribution comparison (Box-Cox)**
- Before: Skewed distributions, non-normal Q-Q plots
- After: Near-normal distributions

**Cell 20: Yeo-Johnson transformation**
- `pt1 = PowerTransformer()` - Default method
- Works with any values (positive or negative)

**Cell 21-22: Model with Yeo-Johnson**
- `pt1.lambdas_` - Learned parameters
- Similar or improved R² compared to Box-Cox

### How Power Transformers Work:
- **Box-Cox:** Finds optimal lambda to achieve target Y = (X^lambda - 1) / lambda
  - Requires X > 0
  - More powerful transformation

- **Yeo-Johnson:** Finds optimal lambda with modified formula
  - Works with negative values
  - More robust to outliers

### Lambda Interpretation:
- λ = 1: No transformation
- λ = 0.5: Square root transformation
- λ = 0: Log transformation
- λ = -1: Reciprocal transformation
- λ optimized: Best for Gaussianity

### When to Use:
- Numerical regression data needing normality
- Right-skewed or severely non-normal distributions
- When standard log/sqrt insufficient
- Before linear regression, LDA, or methods assuming normality

### When NOT to use:
- Tree-based models (already robust)
- When data is already approximately normal
- With extreme outliers (may over-correct)

### Key Methods:
- `PowerTransformer(method='box-cox')` - Box-Cox only
- `PowerTransformer()` - Yeo-Johnson (default)
- `fit_transform()` - Learn and apply
- `transform()` - Apply to new data
- `.lambdas_` - Access learned parameters

### Important Concepts:
- Mathematical search for optimal transformations
- Automatic lambda selection via maximum likelihood
- Improves model performance through better distributions
- Essential preprocessing for assumption-sensitive algorithms
- Fit on training data, apply to test data
