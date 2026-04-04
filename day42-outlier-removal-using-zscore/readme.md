# Day 42 - Outlier Removal Using Z-Score

## Resources
Video Link:https://youtu.be/OnPE-Z8jtqM

---

## Notebook: (main notebook in this folder)

### Lesson Overview
Identify and handle outliers using the statistical Z-score method based on standard deviations.

### Code Cells Explanation:

**Cell 1: Load data**
- `df = pd.read_csv('placement.csv')`

**Cell 2-3: Explore distributions**
- Distribution plots show CGPA and exam marks distributions
- Identify potential outliers visually

**Cell 4: Z-score calculation**
- Z-score = (X - mean) / std
- Standardizes value to number of standard deviations from mean
- Z > 3: Extremely rare (>99.7% of data)
- Z < -3: Normal range for ~99.7% of normal data

**Cell 5-8: Statistical parameters**
- `df['cgpa'].mean()` - Mean
- `df['cgpa'].std()` - Std
- `df['cgpa'].min()` - Min
- `df['cgpa'].max()` - Max

**Cell 9: Calculate outlier boundaries**
- Upper bound = mean + 3×std
- Lower bound = mean - 3×std
- Values outside this range are potential outliers

**Cell 10: Identify outliers**
- Find rows meeting extreme value criteria

### Handling Approach 1: Trimming (Remove Outliers)

**Cell 11: Remove outlier rows**
- Keep only non-outlier rows
- Data loss: Discards observations

### Handling Approach 2: Z-Score Method

**Cell 12-13: Calculate Z-scores**
- Standardize variable
- Outliers: |Z| > 3

**Cell 14-16: Find extreme Z-scores**
- Upper outliers
- Lower outliers

**Cell 17: Trim using Z-scores**
- Remove extreme values

### Handling Approach 3: Capping (Winsorization)

**Cell 18-19: Define limits**
- Upper and lower thresholds

**Cell 20-25: Apply capping with np.where**
- If value > upper_limit: Replace with upper_limit
- Else if value < lower_limit: Replace with lower_limit
- Else: Keep original value

**Cell 26-27: Verify capping**
- Same shape (no data loss)
- Statistics show capping effect

### Comparison of Methods:
1. **Trimming (Deletion):**
   - Pros: Clean dataset, no value distortion
   - Cons: Information loss
   - Use when: Few outliers, can afford loss

2. **Capping (Winsorization):**
   - Pros: Retains observations, preserves relationships
   - Cons: Creates artificial values
   - Use when: Want all data, outliers erroneous

### Key Thresholds:
- |Z| > 2: ~5% outliers (95% within range)
- |Z| > 2.5: ~1.2% outliers
- |Z| > 3: ~0.3% outliers (traditional)

### Important Concepts:
- Outlier detection vs. treatment (separate steps)
- ±3 sigma is traditional but arbitrary
- Must document and justify approach
- Always compare before/after distributions
