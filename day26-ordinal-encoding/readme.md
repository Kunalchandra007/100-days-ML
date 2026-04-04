# Day 26 - Ordinal Encoding

## Resources
Video Link: https://youtu.be/w2GglmYHfmM

---

## Notebook: day26.ipynb

### Lesson Overview
Encode categorical variables with natural ordering as ranked integer values.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import numpy as np, pandas as pd`
- `from sklearn.preprocessing import OrdinalEncoder, LabelEncoder`

**Cell 2: Load data**
- `df = pd.read_csv('customer.csv')`

**Cell 3-4: Explore data**
- `df.sample(5)`, `df.iloc[:,2:]` - Remove ID columns
- Preview customer data

**Cell 5: OrdinalEncoder**
- `from sklearn.preprocessing import OrdinalEncoder`
- Import ordinal encoding class

**Cell 6: Define encoder with categories**
- `oe = OrdinalEncoder(categories=[['Poor','Average','Good'], ['School','UG','PG']])`
- Explicitly define category order:
  - Rating: Poor=0, Average=1, Good=2
  - Education: School=0, UG=1, PG=2
- Order matters! Defines the numeric mapping

**Cell 7: Fit encoder**
- `oe.fit(X_train)` - Learn categories from training data

**Cell 8-9: Transform**
- `X_train = oe.transform(X_train)` - Apply encoding
- Each category replaced with its rank (0, 1, 2, ...)

**Cell 10: View encoded values**
- `X_train` - Shows numeric values 0, 1, 2

**Cell 11: Access categories**
- `oe.categories_` - View learned category ordering

**Cell 12: LabelEncoder**
- `from sklearn.preprocessing import LabelEncoder`
- Alternative for single column encoding

**Cell 13: Create LabelEncoder**
- `le = LabelEncoder()`
- Initialize encoder for target variable

**Cell 14: Fit on target**
- `le.fit(y_train)` - Learn unique classes

**Cell 15: View classes**
- `le.classes_` - Display class mapping

**Cell 16: Transform target**
- `y_train = le.transform(y_train)` - Encode labels
- `y_test = le.transform(y_test)` - Apply same encoding

**Cell 17: View encoded target**
- `y_train` - Shows numeric class labels (0, 1, 2, ...)

### Key Difference from OneHot:
- Ordinal: Preserves ranking relationship (Poor < Average < Good)
- OneHot: Treats categories as unordered (multicollinearity)

### Use Cases:
- Educational level: School < UG < PG (natural order)
- Customer rating: Poor < Average < Good (natural order)
- Any categorical with inherent ordering

### Key Methods:
- `OrdinalEncoder()` - Encode multiple ordinal columns
- `LabelEncoder()` - Encode single column (often targets)
- `fit()` - Learn categories from data
- `transform()` - Apply encoding
- `categories_`, `classes_` - Access learned mappings

### Important Concepts:
- Define order explicitly to preserve ranking
- Different from one-hot encoding (which is unordered)
- Works well with tree-based models
- Linear models interpret ranks as continuous
