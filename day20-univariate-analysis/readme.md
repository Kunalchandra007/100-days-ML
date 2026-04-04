# Day 20 - Univariate Analysis

## Resources
Video Link : https://www.youtube.com/watch?v=4HyTlbHUKSw

---

## Notebook: day20.ipynb

### Lesson Overview
Single variable visualization and analysis techniques for categorical and numerical data.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import pandas as pd, seaborn as sns`

**Cell 2: Load data**
- `df = pd.read_csv('train.csv')`

**Cell 3: Sample data**
- `df.head()` - Preview dataset

**Cell 4: Categorical variable - Count plot**
- `sns.countplot(df['Embarked'])` - Bar chart of category frequencies
- Height represents count of observations per category
- Identifies distribution of categorical variable

**Cell 5: Categorical variable - Pie chart**
- `df['Sex'].value_counts().plot(kind='pie', autopct='%.2f')`
- Circular visualization showing proportions
- `autopct='%.2f'` - Display percentage labels

**Cell 6: Numerical variable - Histogram**
- `plt.hist(df['Age'], bins=5)` - Bar chart of intervals
- `bins=5` - Divide data into 5 equal-width intervals
- Shows frequency distribution

**Cell 7: Numerical variable - Distribution plot**
- `sns.distplot(df['Age'])` - Combines histogram + kernel density estimate (KDE)
- KDE line shows smooth distribution estimate
- Better visualization of data shape

**Cell 8: Numerical variable - Box plot**
- `sns.boxplot(df['Age'])` - Shows box plot with outliers
- Box: 25th-75th percentile (IQR)
- Line in box: median (50th percentile)
- Whiskers: extend to 1.5×IQR
- Points beyond whiskers: outliers

**Cell 9-11: Statistical measures**
- `df['Age'].min()` - Minimum value
- `df['Age'].max()` - Maximum value
- `df['Age'].mean()` - Average value
- `df['Age'].skew()` - Skewness (asymmetry of distribution)
  - Negative: left-skewed
  - Positive: right-skewed
  - Near 0: symmetric

### Key Visualizations:
- Countplot: Categorical frequencies
- Pie chart: Categorical proportions
- Histogram: Numerical distribution (fixed bins)
- Distribution plot: Numerical distribution (smooth estimation)
- Box plot: Quartiles and outliers

### Key Statistics:
- Min, max: Range extremes
- Mean, median, mode: Central tendency
- Std, variance: Spread/dispersion
- Skewness: Distribution asymmetry
- Kurtosis: Distribution tail behavior
