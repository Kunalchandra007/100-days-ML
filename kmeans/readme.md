# K-Means Clustering

Codes related to the K-Means clustering algorithm

---

## Notebook: kmeans-clustering-demo.ipynb

### Lesson Overview
Unsupervised learning algorithm partitioning data into K clusters based on feature similarity.

### Algorithm Steps:

**Step 1: Initialize**
- Choose K initial centroids randomly
- Or use predetermined positions

**Step 2: Assignment**
- Assign each point to nearest centroid
- Create K clusters

**Step 3: Update**
- Recalculate centroids as cluster means
- New centroids: mean of all points in cluster

**Step 4: Iterate**
- Repeat steps 2-3 until convergence
- Convergence: Centroids don't move significantly

### Key Concepts:

**Distance Metric:**
- Euclidean distance: sqrt((x₁-x₂)² + (y₁-y₂)² + ...)
- Closest centroid determines cluster membership

**Inertia:**
- Sum of squared distances to cluster centers
- Lower inertia = tighter clusters
- Used for elbow method

**Elbow Method:**
- Plot inertia vs. K (number of clusters)
- Watch for "elbow" (sharp decrease)
- Choose K at elbow point
- Balances cluster tightness vs. model simplicity

### Implementation:

**Code Pattern:**
```python
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=3, random_state=42)
cluster_labels = kmeans.fit_predict(data)
centroids = kmeans.cluster_centers_
inertia = kmeans.inertia_
```

**Key Methods:**
- `fit()` - Learn centroids
- `predict()` - Assign new data to clusters
- `fit_predict()` - Both fit and predict

**Key Attributes:**
- `.cluster_centers_` - Centroid coordinates
- `.labels_` - Cluster assignment per sample
- `.inertia_` - Sum of squared distances
- `.n_iter_` - Iterations until convergence

### When to Use K-Means:
1. **Customer segmentation:** Group similar customers
2. **Image compression:** Reduce colors via clustering
3. **Anomaly detection:** Identify outlier clusters
4. **Document clustering:** Group similar documents
5. **Preliminary analysis:** Understand data structure

### Advantages:
- Simple and fast
- Scales to large datasets
- Easy to interpret
- Works with any data type (after encoding)

### Disadvantages:
- Must specify K in advance
- Sensitive to initialization
- Assumes spherical clusters
- Struggles with varying density clusters
- Sensitive to outliers

### Comparison with Other Methods:
- **K-Means vs. Hierarchical:** K-Means faster, Hierarchical shows dendrograms
- **K-Means vs. DBSCAN:** K-Means spherical clusters, DBSCAN arbitrary shapes
- **K-Means vs. Gaussian Mixture:** K-Means hard assignment, GMM soft assignment

### Tips for Better Clustering:
1. **Scale features:** Use StandardScaler
2. **Find optimal K:** Use elbow method or silhouette score
3. **Multiple initializations:** Run with n_init > 1
4. **Visualize:** Plot 2D/3D projections
5. **Validate:** Use domain knowledge to verify clusters

### Key Parameters:
- `n_clusters` - Number of clusters (must specify)
- `init` - Initialization method ('k-means++' recommended)
- `random_state` - For reproducibility
- `n_init` - Number of initializations (10 default)
- `max_iter` - Maximum iterations (300 default)

### Convergence Criteria:
- Maximum iterations reached
- Centroids don't change
- Inertia doesn't decrease significantly

### Important Concepts:
- Unsupervised: No target variable
- Partition-based: Hard cluster assignment
- Distance-based: Euclidean distances
- NP-hard problem: No guaranteed optimal solution
- Multiple runs recommended (choose best inertia)
