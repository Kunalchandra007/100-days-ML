# Day 43 - Outlier Removal Using IQR Method

## Resources
Video Link:

---

## Notebook: (main notebook in this folder)

### Lesson Overview
Identify outliers using Interquartile Range method, more robust to extreme values than Z-score.

### Code Cells Explanation:

**Cell 1: Load data**
- `df = pd.read_csv('placement.csv')`

**Cell 2: Explore distributions**
- Box plot and distribution plots

**Cell 3: Statistical summary**
- `df['placement_exam_marks'].describe()` - Shows Q1, median, Q3

**Cell 4: Box plot visualization**
- Visual representation of quartiles

**Cell 5-6: Calculate quartiles**
- `Q1 = df['placement_exam_marks'].quantile(0.25)` - 25th percentile
- `Q3 = df['placement_exam_marks'].quantile(0.75)` - 75th percentile

**Cell 7: Calculate IQR**
- IQR = Q3 - Q1
- Represents middle 50% of data
- Robust measure (unaffected by extremes)

**Cell 8: Outlier boundaries**
- Upper bound = Q3 + 1.5 × IQR
- Lower bound = Q1 - 1.5 × IQR
- Rule of thumb: 1.5 × IQR distance from quartiles

**Cell 9: Identify outliers**
- Find rows beyond boundaries

### Handling Approach 1: Trimming

**Cell 10-11: Remove outliers**
- Keep only values within bounds
- Data loss but clean dataset

**Cell 12: Comparison visualization**
- Before and after distributions

### Handling Approach 2: Capping

**Cell 13-14: Define capping logic**
- Conditional replacement

**Cell 15: Apply capping**
- Replace extreme values with boundaries
- Retain all observations

**Cell 16: Verify capping**
- Same number of observations preserved

**Cell 17: Comparison after capping**
- Before and after comparison

### Why IQR Method?

Advantages over Z-Score:
1. **Distribution-free:** Doesn't assume normality
2. **Robust:** Unaffected by extreme outliers
3. **Non-parametric:** Works with any distribution
4. **Visual:** Box plots show boundaries clearly
5. **Flexible:** Adjust multiplier (1.5, 3.0) as needed

### Adjusting IQR Multiplier:
- 1.5 × IQR: Standard (catches ~0.35% outliers if normal)
- 3.0 × IQR: More conservative (catches extreme outliers)
- 1.0 × IQR: Aggressive (removes many observations)

### Key Methods:
- `.quantile(0.25)` - First quartile (Q1)
- `.quantile(0.75)` - Third quartile (Q3)
- `np.where()` - Conditional replacement
- Box plot visualization confirms outliers

### Important Concepts:
- IQR method most common in practice
- Better than Z-score for non-normal data
- Always visualize before/after results
- Document outlier handling decisions
