# Day 21 - Bivariate Analysis

## Resources
Video link:

---

## Notebook: day21.ipynb

### Lesson Overview
Analyze relationships between two variables using appropriate visualization techniques for different data types.

### Code Cells Explanation:

**Cell 1-3: Load sample datasets**
- `sns.load_dataset('tips')` - Dine-in restaurant tips data
- `sns.load_dataset('flights')` - Airline passenger data
- `sns.load_dataset('iris')` - Iris flower measurements

**Cell 4: Load Titanic data**
- `pd.read_csv('train.csv')` - Custom dataset

**Cell 5: Numerical-Numerical: Scatter plot**
- `sns.scatterplot(tips['total_bill'], tips['tip'])`
- X-Y scatter showing relationship
- `hue=df['sex']` - Color by category
- `style=df['smoker']` - Different point styles
- `size=df['size']` - Point size represents value
- Reveals linear/non-linear relationships, clusters, outliers

**Cell 6-7: Numerical-Categorical: Bar plot**
- `sns.barplot(titanic['Pclass'], titanic['Age'], hue=titanic['Sex'])`
- Average Age per Passenger Class, grouped by Sex
- Bar height = mean value
- `hue` parameter creates grouped bars

**Cell 8: Numerical-Categorical: Box plot**
- `sns.boxplot(titanic['Sex'], titanic['Age'], hue=titanic['Survived'])`
- Age distribution by Sex, separated by Survival status
- Shows quartiles and outliers for each group
- Multiple groupings for complex relationships

**Cell 9: Numerical-Categorical: Overlaid distributions**
- `sns.distplot(titanic[titanic['Survived']==0]['Age'])`
- `sns.distplot(titanic[titanic['Survived']==1]['Age'])`
- Overlay distributions for comparison
- `hist=False` - Show only KDE lines

**Cell 10-11: Categorical-Categorical: Heatmap**
- `pd.crosstab(titanic['Pclass'], titanic['Survived'])`
- `sns.heatmap(crosstab_table)` - Color-coded frequency table
- Color intensity represents cell values
- Easy identification of patterns

**Cell 12: Categorical-Categorical: Cluster map**
- `sns.clustermap(pd.crosstab(titanic['Parch'], titanic['Survived']))`
- Hierarchical clustering visualization
- Rows/columns reordered by similarity
- Row/column dendrograms show clustering

**Cell 13-14: Pairplot for multivariate analysis**
- `sns.pairplot(iris, hue='species')` - All pairwise relationships
- Diagonal: univariate distributions
- Off-diagonal: bivariate scatterplots
- `hue='species'` - Color by category
- Shows all relationships simultaneously

**Cell 15-17: Time series - Line plot**
- `flights.groupby('year').sum()` - Aggregate by year
- `sns.lineplot(year, passengers)` - Time series visualization
- Shows trends over time

### Key Visualization Types:
- Scatter plot: Numerical-Numerical (linear relationships)
- Bar plot: Numerical-Categorical (group comparisons)
- Box plot: Numerical-Categorical (distribution comparison)
- Distribution overlay: Numerical-Categorical (shape comparison)
- Heatmap: Categorical-Categorical (frequency patterns)
- Cluster map: Categorical-Categorical (hierarchical patterns)
- Pairplot: Multivariate (all relationships)
- Line plot: Time series (trends)

### Key Methods:
- `sns.scatterplot()`, `sns.barplot()`, `sns.boxplot()`
- `sns.distplot()`, `sns.heatmap()`, `sns.clustermap()`
- `sns.pairplot()`, `sns.lineplot()`
- `pd.crosstab()` - Contingency tables
- `.groupby().mean()` - Group aggregation
