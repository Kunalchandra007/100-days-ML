# Day 19 - Understanding Your Data - Descriptive Statistics

## Resources
Video Link: https://www.youtube.com/watch?v=mJlRTUuVr04

---

## Notebook: day19.ipynb

### Lesson Overview
Fundamental exploratory data analysis using pandas methods for data profiling and statistical understanding.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import pandas as pd`

**Cell 2: Load data**
- `df = pd.read_csv('train.csv')`

**Cell 3: Dataset dimensions**
- `df.shape` - Returns tuple (number_of_rows, number_of_columns)
- First EDA step to understand dataset size

**Cell 4: Sample data**
- `df.sample(5)` - Display 5 random rows
- Quick visual inspection of data structure

**Cell 5: Data types and info**
- `df.info()` - Display:
  - Column names and data types
  - Non-null counts per column
  - Memory usage

**Cell 6: Missing values**
- `df.isnull().sum()` - Count missing values per column
- Identifies data quality issues

**Cell 7: Descriptive statistics**
- `df.describe()` - Returns DataFrame with:
  - count: number of non-null values
  - mean: average value
  - std: standard deviation
  - min: minimum value
  - 25%, 50%, 75%: percentiles (quartiles)
  - max: maximum value

**Cell 8: Duplicate rows**
- `df.duplicated().sum()` - Count exact duplicate rows
- `df.duplicated(subset=['col1','col2']).sum()` - Duplicates on specific columns

**Cell 9: Correlation analysis**
- `df.corr()['Survived']` - Show correlation coefficients with target variable
- Values range from -1 (negative correlation) to +1 (positive correlation)
- Identifies important predictive features

### Key Methods:
- `df.shape` - Dimensions
- `df.sample()` - Random sampling
- `df.info()` - Comprehensive info
- `df.isnull().sum()` - Missing value count
- `df.describe()` - Statistical summary
- `df.duplicated()` - Find duplicates
- `df.corr()` - Correlation matrix

### Important Concepts:
- Complete data profiling through systematic exploration
- Identification of data quality issues early
- Understanding feature relationships with target
- Statistical measures guide preprocessing decisions
