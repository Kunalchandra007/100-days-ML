# Day 47 - Principal Component Analysis (PCA)

## Resources
PCA code Kaggle notebook : https://www.kaggle.com/nitsin/pca-demo-1
Video Link:https://youtu.be/tXXnxjj2wM4

---

## Notebook: (main notebook in this folder)

### Lesson Overview
Reduce dimensionality while preserving variance using eigenvalue decomposition.

### Code Cells Explanation:

**Cell 1: Generate synthetic data**
- Create 3D synthetic dataset with two classes
- Create 40 samples (20 per class)

**Cell 2: View data**
- Feature1, Feature2, Feature3, Target

**Cell 3: 3D scatter plot**
- Interactive 3D visualization
- Points colored by target class

### PCA Step 1: Standardization

**Cell 4: Standard scaling**
- `StandardScaler().fit_transform(df.iloc[:,0:3])`
- Center: mean = 0, std = 1
- Essential preprocessing for PCA

### PCA Step 2: Covariance Matrix

**Cell 5: Calculate covariance matrix**
- `np.cov([df.col1, df.col2, df.col3])`
- 3×3 symmetric matrix
- Diagonal: Variance of each feature
- Off-diagonal: Covariance between features

### PCA Step 3: Eigenvalue Decomposition

**Cell 6: Find eigenvalues and eigenvectors**
- `eigen_values, eigen_vectors = np.linalg.eig(covariance_matrix)`
- Eigenvalues: Variance explained
- Eigenvectors: Direction of each principal component

**Cell 7: View eigenvalues**
- Largest eigenvalue = maximum variance direction
- Decreasing order: PC1 > PC2 > PC3

**Cell 8: View eigenvectors**
- 3×3 matrix
- Each column: eigenvector (direction)
- Orthogonal: Perpendicular to each other

### PCA Step 4: Visualization of Principal Components

**Cell 9: 3D plot with eigenvectors**
- Plot original data points (scaled)
- Overlay eigenvectors as arrows

### PCA Step 5: Dimensionality Reduction

**Cell 10: Select top components**
- `pc = eigen_vectors[0:2]` - Select first 2 eigenvectors
- Reduce 3D → 2D

**Cell 11: Project data**
- `transformed = np.dot(data, pc.T)` - Matrix multiplication
- Result: 40 samples, 2 components

**Cell 12: Create transformed DataFrame**
- `new_df = pd.DataFrame(transformed, columns=['PC1','PC2'])`

**Cell 13: 2D scatter plot**
- Plot transformed data: PC1 vs PC2
- Classes still well-separated in 2D

### Key Mathematical Concepts:

**Covariance Matrix:** Shows variable relationships

**Eigenvalue Decomposition:** Find principal directions
- A·v = λ·v (Eigenvector equation)

**Projection Formula:**
- Y = X·V (Project features onto eigenvectors)

### PCA Properties:
1. **Orthogonal:** Principal components perpendicular
2. **Ordered:** PC1 > PC2 > PC3 by variance
3. **Uncorrelated:** Components independent
4. **Variance preserving:** Retains most information
5. **Linear:** Linear combination of features

### When to Use PCA:
1. **Dimensionality reduction:** Too many features
2. **Visualization:** Plot high-dimensional data
3. **Reduce computation:** Fewer features → faster
4. **Remove noise:** Ignore low-variance dimensions
5. **Feature extraction:** Create new features

### When NOT to Use PCA:
1. **Interpretability:** Hard to interpret PC meaning
2. **Sparse data:** Assumes dense data
3. **Classification:** May harm separability
4. **Tree models:** Can't benefit from reduction

### Key Methods:
- `np.cov()` - Covariance matrix
- `np.linalg.eig()` - Eigenvalue decomposition
- `np.dot()` - Matrix multiplication (projection)
- `sklearn.decomposition.PCA` - Automated PCA

### Important Concepts:
- Unsupervised: Ignores target variable
- Standardization crucial (scale-dependent)
- Explained variance ratio guides component selection
- Non-linear relationships not captured
