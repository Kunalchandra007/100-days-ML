# Day 25 - Normalization (MinMaxScaler)

## Resources
Video Link: https://youtu.be/eBrGyuA2MIg

---

## Notebook: day25.ipynb

### Lesson Overview
Scale features to fixed range [0, 1] using MinMaxScaler for bounded scaling.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import numpy as np, pandas as pd`
- `from sklearn.preprocessing import MinMaxScaler`

**Cell 2: Load data**
- `df = pd.read_csv('wine_data.csv', header=None, usecols=[0,1,2])`
- Select specific columns from wine dataset

**Cell 3: Rename columns**
- `df.columns=['Class label', 'Alcohol', 'Malic acid']`

**Cell 4: View data**
- `df` - Preview structure

**Cell 5-6: Original distributions**
- `sns.kdeplot(df['Alcohol'])` - Alcohol distribution
- `sns.kdeplot(df['Malic acid'])` - Malic acid distribution
- Different scales, different ranges

**Cell 7: Scatter plot before scaling**
- `sns.scatterplot(df['Alcohol'], df['Malic acid'], hue=df['Class label'])`
- Color by class (1, 2, or 3)

**Cell 8: Train-test split**
- `train_test_split(X, y, test_size=0.3, random_state=0)`

**Cell 9: MinMaxScaler instantiation**
- `scaler = MinMaxScaler()`
- Initialize scaler object

**Cell 10: Fit and transform**
- `scaler.fit(X_train)` - Learn min/max from training data
- `X_train_scaled = scaler.transform(X_train)`
- `X_test_scaled = scaler.transform(X_test)`
- Formula: `(X - min) / (max - min)`
- Results: All values in range [0, 1]

**Cell 11-12: Output statistics**
- `np.round(X_train.describe(), 1)` - Original (Alcohol: 11-13, Malic: 0.74-5.8)
- `np.round(X_train_scaled.describe(), 1)` - Normalized (both 0-1)

**Cell 13: Scatter plot after scaling**
- `scatter(X_train_scaled, ...)`
- Both features now in [0, 1] range

**Cell 14-15: KDE comparison**
- Original: Different ranges, different distributions
- After scaling: Normalized to [0, 1] range
- Shapes preserved, scales unified

### Differences from StandardScaler:
- StandardScaler: mean=0, std=1 (unbounded)
- MinMaxScaler: min=0, max=1 (bounded [0,1])
- MinMaxScaler more intuitive for interpreted ranges
- Both affected by outliers

### When to Use MinMaxScaler:
- Neural Networks (inputs typically [0, 1])
- Image processing (pixel values [0, 255] → [0, 1])
- When bounded range is desired
- When features should be interpreted as probabilities [0, 1]

### Key Concepts:
- Min-Max Normalization: `X_norm = (X - min) / (max - min)`
- Results: min = 0, max = 1 (range [0, 1])
- Preserves shape of original distribution
- Bounded scaling to fixed range
- Fit on training data, apply to test data
- Outlier-sensitive (like StandardScaler)
- For robust handling, use RobustScaler
