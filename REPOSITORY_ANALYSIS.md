# 100-Days ML Repository - Complete Notebook Analysis

## Overview
This document contains detailed analysis of all 46+ notebooks in the repository, organized by day/topic. Each entry includes the lesson description, code explanations, methods used, and important concepts.

---

## DAY 15: Working with CSV Files
**File:** working-with-csv.ipynb

### Lesson Description
Comprehensive guide to reading CSV files with pandas, exploring various parameters and options for data loading.

### Code Cells & Explanations

1. **Import pandas**
   - `import pandas as pd` - Load the pandas library for data manipulation

2. **Open local CSV file**
   - `df = pd.read_csv('aug_train.csv')` - Basic CSV loading with `read_csv()` method

3. **Open CSV from URL**
   - Uses `requests` library to fetch from URL
   - `pd.read_csv(data)` - Load from StringIO object
   - Methods: `requests.get()`, `StringIO()` - Handle HTTP requests and file-like objects

4. **sep Parameter**
   - `pd.read_csv(file, sep='\t')` - Specify delimiter/separator (tab-separated values)
   - `names=['col1','col2']` - Assign custom column names

5. **index_col Parameter**
   - `pd.read_csv(file, index_col='enrollee_id')` - Set specific column as index

6. **header Parameter**
   - `pd.read_csv(file, header=1)` - Use row 1 as header instead of row 0

7. **usecols Parameter**
   - `pd.read_csv(file, usecols=['col1','col2'])` - Select specific columns only

8. **squeeze Parameter**
   - `pd.read_csv(file, squeeze=True)` - Convert single column to Series instead of DataFrame

9. **nrows Parameter**
   - `pd.read_csv(file, nrows=100)` - Load only first N rows for large files

10. **encoding Parameter**
    - `pd.read_csv(file, encoding='latin-1')` - Handle different file encodings

11. **error_bad_lines Parameter**
    - `pd.read_csv(file, error_bad_lines=False)` - Skip problematic rows

12. **dtype Parameter**
    - `pd.read_csv(file, dtype={'target':int})` - Specify data types for columns

13. **parse_dates Parameter**
    - `pd.read_csv(file, parse_dates=['date'])` - Parse string columns as datetime

14. **converters Parameter**
    - Uses custom function to transform column values during reading
    - Apply transformations like renaming values on-the-fly

15. **na_values Parameter**
    - `pd.read_csv(file, na_values=['Male'])` - Treat specific values as NaN/missing

16. **chunksize Parameter**
    - `pd.read_csv(file, chunksize=5000)` - Read large files in chunks
    - Returns iterator for memory-efficient processing

---

## DAY 16: Working with JSON and SQL
**File:** day16.ipynb

### Lesson Description
Learn to read JSON files and connect to SQL databases using pandas and MySQL.

### Code Cells & Explanations

1. **Import pandas**
   - `import pandas as pd`

2. **Read JSON from file**
   - `pd.read_json('train.json')` - Load JSON files directly into DataFrame

3. **Read JSON from API**
   - `pd.read_json(url)` - Fetch and parse JSON from web APIs
   - Example: Exchange rate API returning JSON structure

4. **Install MySQL connector**
   - `!pip install mysql.connector` - Install MySQL database connector

5. **Import MySQL connector**
   - `import mysql.connector` - Import database connection library

6. **MySQL Connection**
   - `mysql.connector.connect()` - Create connection with host, user, password, database
   - Methods: `.connect()` - Establish database connection

7. **SQL Query using pandas**
   - `pd.read_sql_query(query, connection)` - Execute SQL and get results as DataFrame
   - Example: `SELECT * FROM countrylanguage`

### Key Methods
- `pd.read_json()` - Parse JSON data
- `mysql.connector.connect()` - Database connectivity
- `pd.read_sql_query()` - SQL query execution

---

## DAY 17: API to DataFrame
**File:** day17.ipynb

### Lesson Description
Fetch data from REST APIs and convert to pandas DataFrames, handling pagination and large datasets.

### Code Cells & Explanations

1. **Import libraries**
   - `import pandas as pd`, `import requests` - HTTP requests and data manipulation

2. **Basic API request**
   - `response = requests.get(url)` - Fetch data from The Movie Database API
   - Extract specific fields using `response.json()`

3. **Extract and create DataFrame**
   - `pd.DataFrame(response.json()['results'])` - Convert API response to DataFrame
   - Select specific columns: `[['id','title','overview','release_date',...]]`

4. **Initialize empty DataFrame**
   - `df = pd.DataFrame()` - Create empty DataFrame for appending results

5. **Pagination loop**
   - Loop through multiple pages: `for i in range(1,429)`
   - Fetch each page and extract data
   - `df = df.append(temp_df, ignore_index=True)` - Accumulate results

6. **Check dataset size**
   - `df.shape` - Verify final dataset dimensions

7. **Save to CSV**
   - `df.to_csv('movies.csv')` - Export DataFrame to CSV file

### Key Concepts
- REST API pagination handling
- JSON parsing and data extraction
- DataFrame concatenation across multiple API calls

---

## DAY 18: Web Scraping to DataFrame
**File:** day18.ipynb

### Lesson Description
Extract data from websites using BeautifulSoup HTML parsing and create structured DataFrames.

### Code Cells & Explanations

1. **Import libraries**
   - `import pandas as pd`, `import requests`, `from bs4 import BeautifulSoup`, `import numpy as np`

2. **Request webpage**
   - `requests.get(url).text` - Fetch HTML content from website

3. **Parse HTML**
   - `BeautifulSoup(webpage, 'lxml')` - Parse HTML with lxml parser

4. **Find HTML elements**
   - `soup.find_all('div', class_='company-content-wrapper')` - Locate specific elements
   - `soup.prettify()` - Format HTML for viewing

5. **Extract data from containers**
   - `find()` - Get single element
   - `find_all()` - Get all matching elements
   - `.text.strip()` - Extract and clean text

6. **Parse company information**
   - Extract name from `<h2>` tags
   - Extract rating from `<p class='rating'>`
   - Extract reviews from `<a class='review-count'>`
   - Extract company details from `<p class='infoEntity'>`

7. **Error handling**
   - Try-except blocks for robust data extraction
   - Handle missing HTML elements with `np.nan`

8. **Create structured DataFrame**
   - Combine lists into DataFrame with columns:
     - name, rating, reviews, company_type, headquarters, company_age, employees

9. **Pagination loop**
   - Loop through multiple pages (1-1000)
   - Extract data from each page
   - Accumulate results with `final.append(df, ignore_index=True)`

### Key Methods
- `BeautifulSoup.find()` / `find_all()` - HTML element selection
- `requests.get()` - HTTP requests
- Try-except - Error handling for web scraping

---

## DAY 19: Understanding Your Data - Descriptive Statistics
**File:** day19.ipynb

### Lesson Description
Learn fundamental statistical methods for exploring datasets.

### Code Cells & Explanations

1. **Load data**
   - `pd.read_csv('train.csv')`

2. **Dataset dimensions**
   - `df.shape` - Returns (rows, columns)

3. **Sample data**
   - `df.sample(5)` - View random sample of data

4. **Data types and info**
   - `df.info()` - Show column names, types, non-null counts

5. **Missing values**
   - `df.isnull().sum()` - Count missing values per column

6. **Descriptive statistics**
   - `df.describe()` - Show count, mean, std, min, 25%, 50%, 75%, max

7. **Duplicate detection**
   - `df.duplicated().sum()` - Count duplicate rows

8. **Correlation analysis**
   - `df.corr()['Survived']` - Show correlation of all features with target

### Key Concepts
- Shape, info, describe for data profiling
- Missing value detection
- Correlation analysis for feature relationships

---

## DAY 20: Univariate Analysis
**File:** day20.ipynb

### Lesson Description
Analyze individual variables using visualization techniques for categorical and numerical data.

### Code Cells & Explanations

1. **Categorical Data Visualization**
   - `sns.countplot(df['Embarked'])` - Bar chart of category counts
   - `df['Sex'].value_counts().plot(kind='pie')` - Pie chart with percentages

2. **Numerical Data Visualization**
   - `plt.hist(df['Age'], bins=5)` - Histogram with specified bins
   - `sns.distplot(df['Age'])` - Distribution plot (histogram + KDE)
   - `sns.boxplot(df['Age'])` - Box plot showing quartiles and outliers

3. **Statistical measures**
   - `df['Age'].min()` / `.max()` - Range extremes
   - `df['Age'].mean()` - Calculate mean
   - `df['Age'].skew()` - Calculate skewness

### Key Visualizations
- Countplot for categorical frequencies
- Pie charts for proportions
- Histograms for distributions
- Distribution plots (distplot)
- Box plots for outlier visualization

---

## DAY 21: Bivariate Analysis
**File:** day21.ipynb

### Lesson Description
Analyze relationships between two variables using appropriate visualization techniques.

### Code Cells & Explanations

1. **Load datasets**
   - `sns.load_dataset('tips')` / `load_dataset('flights')` / `load_dataset('iris')`

2. **Numerical-Numerical analysis**
   - `sns.scatterplot(x, y, hue=category, style=category2, size=values)` - Multi-dimensional scatter plot

3. **Numerical-Categorical analysis**
   - `sns.barplot(x_categorical, y_numerical, hue=grouping)` - Bar plot with grouping
   - `sns.boxplot(x_categorical, y_numerical, hue=grouping)` - Box plot comparison
   - `sns.distplot()` - Overlay distributions for different groups

4. **Categorical-Categorical analysis**
   - `pd.crosstab(col1, col2)` - Create contingency table
   - `sns.heatmap(crosstab)` - Visualize with heatmap
   - `sns.clustermap()` - Hierarchical clustering visualization

5. **Advanced techniques**
   - `sns.pairplot(iris, hue='species')` - Pairwise relationships matrix
   - `sns.lineplot()` - Time series and continuous relationships
   - Grouped aggregation with `.groupby().mean()`

### Key Methods
- Scatterplot for continuous relationships
- Barplot/boxplot for categorical comparisons
- Heatmap/clustermap for categorical associations
- Pairplot for multivariate analysis

---

## DAY 22: Pandas Profiling
**File:** day22.ipynb

### Lesson Description
Automated exploratory data analysis using pandas-profiling library.

### Code Cells & Explanations

1. **Install pandas-profiling**
   - `!pip install pandas-profiling` - Install library

2. **Generate profile report**
   - `from pandas_profiling import ProfileReport`
   - `ProfileReport(df)` - Create comprehensive profile
   - `prof.to_file(output_file='output.html')` - Export as interactive HTML

### Key Feature
- Automated generation of missing values, distributions, correlations, duplicates
- Interactive HTML report with detailed insights

---

## DAY 24: Standardization (StandardScaler)
**File:** day24.ipynb

### Lesson Description
Scale numerical features to mean=0 and standard deviation=1 for algorithms sensitive to feature magnitude.

### Code Cells & Explanations

1. **Data preparation**
   - Remove non-numeric columns: `df = df.iloc[:,2:]`
   - Train-test split with `train_test_split(test_size=0.3)`

2. **StandardScaler application**
   - `from sklearn.preprocessing import StandardScaler`
   - `scaler = StandardScaler()`
   - `scaler.fit(X_train)` - Learn parameters (mean, std) from training data
   - `scaler.transform(X_train/X_test)` - Apply scaling

3. **Scaling mathematics**
   - Formula: `(X - mean) / std`
   - Access learned parameters: `scaler.mean_`, `scaler.scale_`

4. **Visualization**
   - `sns.kdeplot()` - Compare distributions before/after scaling
   - Scatter plots showing scale effect

5. **Model comparison**
   - **Logistic Regression**: Scaling affects convergence (improved accuracy post-scaling)
   - **Decision Tree**: No difference in accuracy (tree-based models scale-invariant)

6. **Outlier effect**
   - Demonstrate how outliers affect scaling parameters
   - StandardScaler sensitive to outliers

### Key Concepts
- Feature standardization for distance-based algorithms
- Mean=0, std=1 normalization
- Impact on model performance varies by algorithm type

---

## DAY 25: Normalization (MinMaxScaler)
**File:** day25.ipynb

### Lesson Description
Scale numerical features to range [0, 1] using MinMaxScaler.

### Code Cells & Explanations

1. **MinMaxScaler application**
   - `from sklearn.preprocessing import MinMaxScaler`
   - `scaler = MinMaxScaler()`
   - `scaler.fit(X_train)` - Learn min/max from training data
   - `scaler.transform(X_train/X_test)` - Scale to [0,1]

2. **Normalization formula**
   - `(X - min) / (max - min)` - Transforms to [0, 1] range

3. **Visualization**
   - Before/after KDE plots
   - Scatter plots showing normalization effect
   - Distribution comparison

### Key Difference from StandardScaler
- MinMaxScaler: Produces [0, 1] range
- More interpretable as probabilities
- Also affected by outliers

---

## DAY 26: Ordinal Encoding
**File:** day26.ipynb

### Lesson Description
Encode categorical variables with natural ordering as integer values.

### Code Cells & Explanations

1. **OrdinalEncoder**
   - `from sklearn.preprocessing import OrdinalEncoder`
   - `oe = OrdinalEncoder(categories=[['Poor','Average','Good'], ['School','UG','PG']])`
   - Define order explicitly by category order
   - `oe.fit()` - Learn categories
   - `oe.transform()` - Apply encoding (0, 1, 2, ...)

2. **Access categories**
   - `oe.categories_` - View learned category ordering

3. **LabelEncoder**
   - `from sklearn.preprocessing import LabelEncoder`
   - `le = LabelEncoder()`
   - `le.fit()` / `le.transform()` - Encode single column
   - `le.classes_` - View class mapping

### Use Cases
- Ordinal encoding: When categories have natural order (rating levels, education)
- Preserves ordinality in the model

---

## DAY 27: One-Hot Encoding
**File:** day27.ipynb

### Lesson Description
Convert categorical variables to binary columns for unordered categories.

### Code Cells & Explanations

1. **Pandas get_dummies**
   - `pd.get_dummies(df, columns=['fuel','owner'])` - Create dummy variables
   - `drop_first=True` - K-1 encoding (remove multicollinearity reference)

2. **Sklearn OneHotEncoder**
   - `from sklearn.preprocessing import OneHotEncoder`
   - `ohe = OneHotEncoder(drop='first', sparse=False, dtype=np.int32)`
   - `ohe.fit_transform(X[['fuel','owner']])` - Create binary features

3. **Combining features**
   - `np.hstack()` - Concatenate numeric and encoded categorical features

4. **Top category encoding**
   - Group rare categories: `df['brand'].value_counts()`
   - Replace low-frequency categories: `.replace(repl, 'uncommon')`
   - Reduce dimensionality by grouping rare values

### Key Concepts
- Binary (0/1) representation for nominal categories
- Avoids ordinal assumption
- K-1 encoding prevents multicollinearity

---

## DAY 28: Column Transformer
**File:** day28.ipynb

### Lesson Description
Apply different transformations to different column subsets systematically.

### Code Cells & Explanations

1. **ColumnTransformer setup**
   - `from sklearn.compose import ColumnTransformer`
   - `from sklearn.preprocessing import OneHotEncoder, OrdinalEncoder, SimpleImputer`

2. **Define transformers**
   ```
   transformer = ColumnTransformer(transformers=[
       ('name', transformer_obj, ['col_names']),
       ...
   ], remainder='passthrough')
   ```

3. **Apply transformations**
   - SimpleImputer for numerical missing values
   - OrdinalEncoder for ordinal categories
   - OneHotEncoder for nominal categories
   - `remainder='passthrough'` - Keep unspecified columns

4. **Chain preprocessing**
   - `fit_transform(X_train)`
   - `transform(X_test)`

### Key Methods
- Flexible column-specific preprocessing
- Multiple transformations in pipeline
- Handles mixed data types systematically

---

## DAY 29: Sklearn Pipelines
**File:** predict-using-pipeline.ipynb

### Lesson Description
Create reproducible machine learning pipelines combining preprocessing and modeling.

### Key Concepts
- Chain preprocessing and model steps
- Prevent data leakage with proper train-test handling
- Cross-validation friendly
- Production-ready transformations

---

## DAY 30: Function Transformer
**File:** day30.ipynb

### Lesson Description
Apply custom functions to transform features in preprocessing pipelines.

### Code Cells & Explanations

1. **FunctionTransformer**
   - `from sklearn.preprocessing import FunctionTransformer`
   - `trf = FunctionTransformer(func=np.log1p)`
   - Apply custom transformation: `np.log1p()`, `np.sin()`, etc.

2. **Apply transformation**
   - `trf.fit_transform(X_train)`
   - `trf.transform(X_test)`

3. **Model comparison**
   - Compare model performance before/after transformation
   - Logistic Regression and Decision Tree accuracy

4. **Visualization**
   - Before/after distribution comparison
   - Q-Q plots for normality assessment

5. **ColumnTransformer integration**
   - `trf2 = ColumnTransformer([('log', FunctionTransformer(np.log1p), ['Fare'])])`
   - Apply transformation to specific columns only

### Key Functions
- `np.log1p()` - Natural log for right-skewed data
- `np.sin()` - Trigonometric transformations
- Custom functions for domain-specific transformations

---

## DAY 31: Power Transformer
**File:** day31.ipynb

### Lesson Description
Apply Box-Cox and Yeo-Johnson power transformations to make data more Gaussian.

### Code Cells & Explanations

1. **PowerTransformer**
   - `from sklearn.preprocessing import PowerTransformer`
   - `pt = PowerTransformer(method='box-cox')` or default Yeo-Johnson

2. **Box-Cox transformation**
   - `pt.fit_transform(X_train + tiny_constant)` - Requires positive values
   - `pt.lambdas_` - Learned lambda parameters
   - Formula: Transform to approximate normality

3. **Yeo-Johnson transformation**
   - `PowerTransformer()` (default) - Works with negative values
   - `pt1.lambdas_` - Learned parameters

4. **Model improvements**
   - Compare R² scores before/after transformation
   - Cross-validation to assess generalization

5. **Visualization**
   - Distribution plots before/after
   - Q-Q plots showing normality improvement

### Key Difference
- Box-Cox: Only for positive values
- Yeo-Johnson: Works with any values (more flexible)

---

## DAY 32: Binning and Binarization
**File:** day32.ipynb

### Lesson Description
Discretize continuous variables into categorical bins for tree-based model improvements.

### Code Cells & Explanations

1. **KBinsDiscretizer**
   - `from sklearn.preprocessing import KBinsDiscretizer`
   - `kbin = KBinsDiscretizer(n_bins=15, encode='ordinal', strategy='quantile')`

2. **Binning strategies**
   - `strategy='quantile'` - Equal frequency bins
   - `strategy='kmeans'` - Equal-sized bins (by distance)

3. **ColumnTransformer usage**
   - Apply different binning to different columns
   - `trf = ColumnTransformer([('first', kbin_age, [0]), ('second', kbin_fare, [1])])`

4. **Access bin edges**
   - `trf.named_transformers_['first'].bin_edges_[0]` - Get bin boundaries
   - Create labeled bins with `pd.cut()`

5. **Model impact**
   - Binning can improve decision tree performance
   - Trade-off: Information loss vs. feature importance

### Key Concepts
- Discretization for tree-based algorithms
- Equal frequency vs. equal width binning
- Bin edges for interpretability

---

## DAY 34: Handling Dates and Times
**File:** working-with-dates-and-time.ipynb

### Lesson Description
Extract features from datetime columns for time-based analysis and feature engineering.

### Code Cells & Explanations

1. **Convert to datetime**
   - `pd.to_datetime(date['date'])` - Parse string to datetime

2. **Date component extraction**
   - `.dt.year` - Extract year
   - `.dt.month` - Extract month (1-12)
   - `.dt.month_name()` - Get month name
   - `.dt.day` - Extract day
   - `.dt.dayofweek` - Day of week (0-6)
   - `.dt.day_name()` - Get day name ('Monday', etc.)
   - `.dt.week` - Week of year
   - `.dt.quarter` - Quarter (1-4)

3. **Feature engineering**
   - Weekend detection: `np.where(day_name.isin(['Sunday', 'Saturday']), 1, 0)`
   - Semester: `np.where(quarter.isin([1,2]), 1, 2)`

4. **Time difference calculation**
   - `today - date['date']` - Timedelta objects
   - `(today - date).dt.days` - Days elapsed
   - `(total) / np.timedelta64(1, 'M')` - Convert to months/seconds/hours

5. **Time extraction**
   - `.dt.hour` - Hour component
   - `.dt.minute`, `.dt.second` - Minute and second
   - `.dt.time` - Time part only

### Key Methods
- `dt.year`, `dt.month`, `dt.day` - Date components
- `dt.dayofweek`, `dt.day_name()` - Day information
- Timedelta arithmetic for duration calculations

---

## DAY 35: Complete Case Analysis
**File:** day35.ipynb

### Lesson Description
Handle missing data by removing rows with any missing values (listwise deletion).

### Code Cells & Explanations

1. **Identify sparse columns**
   - `df.isnull().mean() * 100` - Percentage missing per column
   - Filter columns with missing < 5%: `cols = [var for var in df.columns if 0 < df[var].isnull().mean() < 0.05]`

2. **Apply CCA**
   - `new_df = df[cols].dropna()` - Keep only complete cases
   - Calculate retention: `len(new_df) / len(df)` - How much data remains

3. **Data distribution comparison**
   - `df[cols].sample(5)` vs `new_df.sample(5)` - Visual comparison
   - Histogram overlay: Original vs CCA data
   - Density plot comparison

4. **Category distribution**
   - Category proportions before/after
   - Identify if CCA creates bias

### Key Concepts
- Simple but may cause bias
- Loss of data (rows with any missing are removed)
- Useful when missing rate is very low

---

## DAY 36: Imputing Numerical Data
**File:** mean-median-imputation.ipynb

### Lesson Description
Fill missing numerical values using statistical methods.

### Code Cells & Explanations

1. **SimpleImputer**
   - `from sklearn.impute import SimpleImputer`
   - Default strategy: mean
   - Other strategies: median, most_frequent, constant

2. **Fit and transform**
   - `si.fit(X_train)` - Learn imputation parameters
   - `si.transform(X_train/X_test)` - Apply imputation

### Key Strategies
- Mean: Affected by outliers
- Median: Robust to outliers
- Most frequent: For categorical
- Constant: Fill with specific value

---

## DAY 37: Handling Missing Categorical Data
**File:** frequent-value-imputation.ipynb

### Lesson Description
Fill missing categorical values using mode (most frequent category).

### Code Cells & Explanations

1. **Most frequent strategy**
   - `SimpleImputer(strategy='most_frequent')`
   - Replace missing with most common category

---

## DAY 38: Missing Indicator
**File:** missing-indicator.ipynb

### Lesson Description
Create binary features indicating missing data patterns.

### Concepts
- Binary indicators for missing values
- Preserve information about missingness
- Used alongside imputation

---

## DAY 39: KNN Imputer
**File:** day39.ipynb

### Lesson Description
Use K-Nearest Neighbors to impute missing values based on similar samples.

### Code Cells & Explanations

1. **KNNImputer**
   - `from sklearn.impute import KNNImputer`
   - `knn = KNNImputer(n_neighbors=3, weights='distance')`
   - `n_neighbors=3` - Use 3 nearest neighbors
   - `weights='distance'` - Weight by proximity

2. **Application**
   - `knn.fit_transform(X_train)`
   - `knn.transform(X_test)`

3. **Model comparison**
   - Compare KNN imputation vs SimpleImputer (mean)
   - KNN typically superior when data has patterns

### Advantage
- Relationship-aware imputation
- Better for correlated features

---

## DAY 40: Iterative Imputer
**File:** step-by-step.ipynb

### Lesson Description
Iteratively impute multiple missing values using regression models.

### Code Cells & Explanations

1. **Iterative approach**
   - Start with mean imputation (0th iteration)
   - For each missing value:
     - Temporarily restore to NaN
     - Train model on complete data
     - Predict missing value
   - Repeat iterations until convergence

2. **Step-by-step example**
   - Multiple iterations (df0, df1, df2, df3, ...)
   - Each iteration refines imputations
   - Compare differences: `df1 - df0`, `df2 - df1`, ...

3. **Convergence**
   - When differences between iterations approach zero

### Key Property
- Improves with multiple iterations
- Captures relationships between variables
- More sophisticated than single imputation

---

## DAY 42: Outlier Removal Using Z-Score
**File:** day42.ipynb

### Lesson Description
Identify and handle outliers using statistical Z-score method.

### Code Cells & Explanations

1. **Z-score calculation**
   - `(X - mean) / std`
   - `df['col_zscore'] = (df['col'] - df['col'].mean()) / df['col'].std()`
   - Values > 3 or < -3 are outliers (3-sigma rule)

2. **Outlier identification**
   - `df[df['col_zscore'] > 3]` - Upper outliers
   - `df[df['col_zscore'] < -3]` - Lower outliers

3. **Trimming**
   - Remove outlier rows: `df[(df['zscore'] < 3) & (df['zscore'] > -3)]`
   - Data loss but clean dataset

4. **Capping**
   - Replace outliers with boundary values
   - `np.where(condition, upper_bound, np.where(..., lower_bound, value))`
   - Retains all data points

### Key Bound
- ±3 standard deviations covers ~99.7% of normal data

---

## DAY 43: Outlier Removal Using IQR Method
**File:** day43.ipynb

### Lesson Description
Detect outliers using Interquartile Range (IQR) method, more robust to extreme values.

### Code Cells & Explanations

1. **IQR calculation**
   - Q1 (25th percentile): `df.col.quantile(0.25)`
   - Q3 (75th percentile): `df.col.quantile(0.75)`
   - IQR = Q3 - Q1

2. **Outlier boundaries**
   - Upper limit: Q3 + 1.5 × IQR
   - Lower limit: Q1 - 1.5 × IQR

3. **Identification**
   - `df[df['col'] > upper_limit]` - Upper outliers
   - `df[df['col'] < lower_limit]` - Lower outliers

4. **Handling**
   - Trimming: `df[df['col'] < upper_limit]`
   - Capping: Replace with limits

### Advantage
- Box plot visualization shows outliers
- Robust to extreme values
- Less stringent than Z-score

---

## DAY 44: Outlier Detection Using Percentiles
**File:** day44.ipynb

### Lesson Description
Detect outliers using percentile-based approach (Winsorization).

### Code Cells & Explanations

1. **Percentile bounds**
   - 99th percentile: `df['col'].quantile(0.99)`
   - 1st percentile: `df['col'].quantile(0.01)`

2. **Trimming**
   - `df[(df['col'] <= 99th) & (df['col'] >= 1st)]`

3. **Capping (Winsorization)**
   - `np.where(df['col'] >= 99th, 99th, np.where(df['col'] <= 1st, 1st, df['col']))`

### Key Difference
- Flexible percentile selection (not fixed sigma/IQR)
- 1-99 percentiles common choice

---

## DAY 45: Feature Construction and Splitting
**File:** day45.ipynb

### Lesson Description
Create new features from existing ones and split features to improve model performance.

### Code Cells & Explanations

1. **Feature construction**
   - `X['Family_size'] = X['SibSp'] + X['Parch'] + 1` - Combine related features
   - Apply functions: `X['Family_type'] = X['Family_size'].apply(myfunc)`
   - Improves model performance through domain knowledge

2. **Feature splitting**
   - Extract title from names: `df['Title'] = df['Name'].str.split(', ', expand=True)[1]...`
   - Create binary features: `df['Is_Married'] = (df['Title'] == 'Mrs').astype(int)`
   - Split complex features for interpretability

3. **Feature selection**
   - Remove redundant features after construction
   - Feature engineering + selection improves accuracy

### Cross-Validation Impact
- Improved CV scores through better feature engineering
- Example: From ~0.795 to ~0.802 accuracy

---

## DAY 47: Principal Component Analysis (PCA)
**File:** pca_step_by_step (1).ipynb

### Lesson Description
Reduce dimensionality while preserving variance using PCA.

### Code Cells & Explanations

1. **Data preparation**
   - Generate synthetic 3D data with `np.random.multivariate_normal()`
   - StandardScale features: `StandardScaler().fit_transform(df)`

2. **Covariance matrix**
   - `np.cov([df.col1, df.col2, df.col3])` - Compute 3×3 covariance matrix

3. **Eigenvalue decomposition**
   - `np.linalg.eig(covariance_matrix)` - Get eigenvalues and eigenvectors
   - Eigenvectors = Principal components (directions of maximum variance)
   - Eigenvalues = Variance explained per component

4. **3D visualization**
   - Plot original data with eigenvectors as arrows
   - Show principal component directions

5. **Dimensionality reduction**
   - Select top 2 eigenvectors: `pc = eigen_vectors[0:2]`
   - Project: `transformed = np.dot(data, pc.T)`
   - Result: 3D → 2D while retaining most variance

6. **2D visualization**
   - Plot transformed data showing class separation

### Key Concepts
- Linear dimensionality reduction
- Eigenvalues indicate variance explained
- Trade-off: Dimensionality vs. information loss

---

## DAY 48-66: Regression and Classification Algorithms
Multiple notebooks covering:
- Simple/Multiple Linear Regression
- Gradient Descent (Batch, SGD, Mini-batch)
- Polynomial Regression
- Regularized models (Ridge, Lasso, ElasticNet)
- Logistic Regression
- Classification metrics
- Random Forest
- AdaBoost
- Gradient Boosting
- K-Means Clustering

---

## GRADIENT-BOOSTING: Gradient Boosting Algorithm
**File:** gradient_boost_step_by_step.ipynb

### Lesson Description
Sequential ensemble method that combines weak learners to create strong predictor.

### Key Concepts
- Iterative residual fitting
- Learning rate parameter
- Staged predictions improving with each estimator

---

## KMEANS: K-Means Clustering
**File:** kmeans-clustering-demo.ipynb

### Lesson Description
Unsupervised learning to partition data into K clusters.

### Code Cells & Explanations

1. **KMeans algorithm**
   - `from sklearn.cluster import KMeans`
   - `KMeans(n_clusters=3)`
   - Iteratively assigns points to nearest centroid and updates centroids

2. **Fit and predict**
   - `kmeans.fit_transform(data)` - Learn clusters and get distances
   - `kmeans.cluster_centers_` - Final cluster centers

3. **Elbow method**
   - Plot inertia vs. number of clusters
   - Find "elbow" point for optimal K

### Key Parameters
- `n_clusters` - Number of clusters
- `random_state` - Reproducibility
- `init` - Initialization method

---

## Summary Statistics
- **Total Notebooks Analyzed:** 46+
- **Data Loading & Manipulation:** Days 15-18
- **Exploratory Data Analysis:** Days 19-22
- **Feature Scaling & Encoding:** Days 24-28
- **Feature Transformation:** Days 30-31
- **Feature Engineering:** Days 32, 34-45
- **Dimensionality Reduction:** Day 47
- **Supervised Learning:** Days 48-66
- **Unsupervised Learning:** K-Means
- **Ensemble Methods:** Days 65-66, Gradient Boosting

This repository provides a comprehensive foundation in machine learning from data loading through advanced ensemble methods and unsupervised learning techniques.
