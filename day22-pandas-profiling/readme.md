# Day 22 - Pandas Profiling

## Resources
Video Link:https://www.youtube.com/watch?v=E69Lg2ZgOxg

---

## Notebook: day22.ipynb

### Lesson Overview
Automated exploratory data analysis generating comprehensive reports.

### Code Cells Explanation:

**Cell 1: Load data**
- `df = pd.read_csv('train.csv')`

**Cell 2: Preview data**
- `df.head()` - First few rows

**Cell 3: Install pandas-profiling**
- `!pip install pandas-profiling` - Install automated EDA library

**Cell 4: Generate profile report**
- `from pandas_profiling import ProfileReport`
- `prof = ProfileReport(df)` - Create comprehensive analysis
- `prof.to_file(output_file='output.html')` - Export as interactive HTML

### Report Contents:
- Overview: Dataset dimensions, memory usage
- Variable types: Numerical, categorical, datetime, etc.
- Missing values: Count and visualizations
- Duplicates: Detection and visualization
- Statistical summaries: Min, max, mean, median, etc.
- Correlations: Feature relationships and heatmaps
- Histograms: Distribution visualization
- Value counts: Categorical frequencies
- Interactions: Bivariate relationships
- Missing data patterns: Heatmap of missingness

### Advantages:
- One-click comprehensive EDA
- Interactive HTML report
- Professional visualization
- Instant insights without manual coding
- Ideal for quick data profiling
