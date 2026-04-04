# Day 45 - Feature Construction and Feature Splitting

## Resources
Video Link https://youtu.be/ma-h30PoFms

---

## Notebook: (main notebook in this folder)

### Lesson Overview
Create new features from existing ones and split complex features to improve model performance.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `from sklearn.model_selection import cross_val_score`
- `from sklearn.linear_model import LogisticRegression`

**Cell 2: Load data**
- `df = pd.read_csv('train.csv')[['Age','Pclass','SibSp','Parch','Survived']]`
- Select relevant Titanic columns

**Cell 3: Prepare data**
- `df.dropna(inplace=True)` - Remove missing values

**Cell 4-5: Create variables**
- `X = df.iloc[:, 0:4]` - Features
- `y = df.iloc[:, -1]` - Target (Survived)

**Cell 6: Baseline model**
- Baseline accuracy: ~0.795

### Feature Construction

**Cell 7: Combine related features**
- `X['Family_size'] = X['SibSp'] + X['Parch'] + 1`
- Create new feature from existing ones
- Total family size on ship

**Cell 8: View constructed feature**
- `X.head()` - Shows new Family_size column

**Cell 9-14: Create categorical feature from numerical**
- Define function for categorization
- Domain knowledge: Family size categories matter for survival

**Cell 15: Apply function**
- `X['Family_type'] = X['Family_size'].apply(myfunc)`
- Categorical feature: 0 (alone), 1 (small), 2 (large)

**Cell 16: View engineered features**
- Shows both Family_size and Family_type

**Cell 17: Remove redundant features**
- SibSp/Parch now redundant

**Cell 18: Updated features**
- Now has Age, Pclass, Family_type

**Cell 19: Improved model**
- New accuracy: ~0.803
- Feature engineering improved model! (+0.8%)

### Feature Splitting (Extracting from Complex Features)

**Cell 20: Load full dataset**
- Access Name column

**Cell 21: View names**
- Format: "LastName, Title. FirstName"

**Cell 22: Extract title**
- Split by comma, get middle part (title)
- Examples: Mr., Mrs., Miss., Dr., etc.

**Cell 23: Verify extraction**
- Shows extracted titles

**Cell 24: View names and titles**
- Side-by-side comparison

**Cell 25: Survival by title**
- Shows survival rates by title
- Titles predictive of survival

**Cell 26-27: Create binary feature**
- `df['Is_Married'] = 0` - Initialize
- Set married (Mrs) = 1
- Binary feature: 1 if married, 0 otherwise

**Cell 28: View engineered feature**
- Shows binary values

### Advantages of Feature Engineering:
1. **Domain knowledge:** Incorporate human understanding
2. **Model improvement:** Often 1-5% accuracy gain
3. **Interpretability:** New features more meaningful
4. **Feature reduction:** Combine multiple features
5. **Capture relationships:** Create interaction terms

### Feature Construction Techniques:
1. **Arithmetic operations:** Sum, difference, ratio, product
2. **Binning:** Group continuous into categorical
3. **Aggregation:** Groups, rolling windows
4. **Encoding:** Convert categorical to numerical
5. **Interaction:** Combine two features

### Important Concepts:
- Feature engineering crucial for model performance
- Domain expertise guides feature creation
- Always cross-validate improvements
- Document feature engineering decisions
- Remove/consolidate redundant features
