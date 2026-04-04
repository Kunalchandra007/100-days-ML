# Day 24 - Standardization (StandardScaler)

## Resources
Video Link : https://youtu.be/1Yw9sC0PNwY

---

## Notebook: day24.ipynb

### Lesson Overview
Scale features to mean=0 and std=1 for distance-based and gradient descent algorithms.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import numpy as np, pandas as pd, seaborn as sns, matplotlib.pyplot as plt`
- `from sklearn.model_selection import train_test_split`
- `from sklearn.preprocessing import StandardScaler`

**Cell 2: Load data**
- `df = pd.read_csv('Social_Network_Ads.csv')`

**Cell 3: Remove ID columns**
- `df = df.iloc[:, 2:]` - Keep only feature columns

**Cell 4: Sample data**
- `df.sample(5)` - Preview

**Cell 5: Train-test split**
- `train_test_split(X, y, test_size=0.3, random_state=0)`
- 70% training, 30% testing data
- `random_state=0` for reproducibility

**Cell 6: StandardScaler instantiation**
- `scaler = StandardScaler()`
- Initialize scaler object

**Cell 7: Fit scaler on training data**
- `scaler.fit(X_train)` - Learn mean and std from training data
- **Critical:** Fit ONLY on training data to prevent data leakage

**Cell 8-9: Transform data**
- `X_train_scaled = scaler.transform(X_train)`
- `X_test_scaled = scaler.transform(X_test)`
- Formula: `(X - mean) / std`
- Results: mean ≈ 0, std ≈ 1

**Cell 10: View scaling parameters**
- `scaler.mean_` - Learned mean values
- `scaler.scale_` - Learned standard deviations

**Cell 11-12: Compare before/after**
- Original X_train (e.g., Age 18-85, Salary 15000-150000)
- Scaled X_train_scaled (e.g., Age -2 to +2, Salary -2 to +2)
- Different scales normalized to similar ranges

**Cell 13-14: Output statistics**
- `np.round(X_train.describe(), 1)` - Original statistics
- `np.round(X_train_scaled.describe(), 1)` - Scaled statistics

**Cell 15: Visualization before scaling**
- Scatter plot Age vs Salary before scaling
- Age range: 18-85, Salary range: 15K-150K
- Vastly different scales

**Cell 16: Visualization after scaling**
- Scatter plot after StandardScaler
- Both features now have similar scales (-3 to +3)
- Equal axis scaling emphasizes relationships

**Cell 17-18: KDE comparison**
- Shows distribution overlap before/after
- Standardized distributions centered at 0

**Cell 19: Model comparison - Logistic Regression**
- `lr = LogisticRegression()`
- Train on original vs scaled data
- Compare accuracy scores
- Expected: Scaling improves gradient descent convergence

**Cell 20-22: Decision Tree comparison**
- Decision trees are scale-invariant
- No performance difference before/after scaling
- Tree-based models don't require scaling

### When to Use StandardScaler:
- Logistic Regression (gradient descent)
- Linear/Ridge/Lasso Regression
- KNN (distance-based)
- K-Means (distance-based)
- Neural Networks
- SVM (distance-based)

### When NOT needed:
- Decision Trees (scale-invariant)
- Random Forests (scale-invariant)
- Gradient Boosting (internal scaling)

### Key Concepts:
- Standardization: `Z = (X - mean) / std`
- Results: mean = 0, std = 1
- Fit on training data ONLY (prevent leakage)
- Apply same transformation to test data
- Enables fair feature importance comparison
- Essential for convergence of gradient descent
