# Day 44 - Outlier Detection Using Percentiles

## Resources
Video Link :

---

## Notebook: (main notebook in this folder)

### Lesson Overview
Detect outliers using percentile-based approach (Winsorization) for flexible threshold selection.

### Code Cells Explanation:

**Cell 1: Load data**
- `df = pd.read_csv('weight-height.csv')`

**Cell 2-3: Explore data**
- `df.head()` - Preview
- `df.shape` - Dataset dimensions

**Cell 4-5: Statistical summary**
- `df['Height'].describe()` - Shows quartiles

**Cell 6: Visualize distribution**
- `sns.distplot(df['Height'])` - Distribution plot

**Cell 7: Box plot**
- Shows quartiles visually

### Percentile-Based Approach

**Cell 8: Set upper percentile**
- `upper_limit = df['Height'].quantile(0.99)` - 99th percentile
- Only ~1% of data above this threshold

**Cell 9: Set lower percentile**
- `lower_limit = df['Height'].quantile(0.01)` - 1st percentile
- Only ~1% of data below this threshold

### Handling Approach 1: Trimming

**Cell 10-15: Remove extreme values**
- Keep only central 98% of data
- Comparison statistics before/after

**Cell 16-17: Visualize trimmed data**
- Trimmed distribution visualization
- Narrower range

### Handling Approach 2: Capping (Winsorization)

**Cell 18: Apply capping**
- If value ≥ upper_limit: Replace with upper_limit
- Else if value ≤ lower_limit: Replace with lower_limit
- Else: Keep original

**Cell 19: Verify capping**
- Same number of observations preserved

**Cell 20-21: Visualize capped data**
- Capped distribution visualization
- Values bounded

### Why Percentile-Based Method?

Advantages:
1. **Flexibility:** Choose any percentile thresholds
2. **Intuitive:** Often use 1-99 percentiles (exclude 1% each tail)
3. **Data-driven:** Automatically adapts to data
4. **Visual:** Box and distribution plots show results
5. **No assumptions:** Works with any distribution

### Common Percentile Choices:
- 1-99: Very conservative (keep central 98%)
- 2.5-97.5: Moderate (keep central 95%)
- 5-95: Aggressive (keep central 90%)
- Custom: Domain-specific thresholds

### Key Methods:
- `.quantile(p)` - Get pth percentile
- `np.where()` - Conditional replacement
- `sns.distplot()`, `sns.boxplot()` - Visualization

### Important Concepts:
- Percentile-based most flexible approach
- Often 1st and 99th percentiles for symmetry
- Can use different percentiles for each tail
- Winsorization: Cap instead of remove
- Always compare before/after distributions 
