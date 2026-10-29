# open-world-category-discovery

## Objective

Use K-Means to perform unsupervised clustering on two-dimensional synthetic data.

## Method

- Generate **400 data points** with `sklearn.datasets.make_blobs` (4 true centers, `cluster_std=1.2`, `random_state=42`).
- Fit K-Means with **K = 3** and **K = 4** (`n_init=10`, `random_state=42`).
- Compare the two models using **inertia** (within-cluster sum of squared distances).

## Results

| K | Inertia |
|---|---------|
| 3 | **3218.6614** |
| 4 | **1103.7864** |

**K = 3**

![K-Means clustering with K=3](experiments/figures/kmeans_k3.png)

**K = 4**

![K-Means clustering with K=4](experiments/figures/kmeans_k4.png)

## Observation

The K=3 model has a much larger inertia (3218.66) than the K=4 model (1103.79). Inertia is the sum of squared distances between every point and the centroid of its assigned cluster, and K-Means minimizes exactly this quantity. When K increases, there is one more centroid available, so a point that was far from its K=3 centroid can be reassigned to a closer center. The minimum total distance can therefore only decrease or stay the same. In this experiment the data were generated from four clusters, so K=3 is forced to merge two of them, leaving large within-cluster distances. K=4 matches the underlying structure and reduces the inertia substantially. However, a lower inertia does not automatically mean a better clustering: inertia generally decreases as K grows, so choosing K should also consider methods such as the elbow method or silhouette analysis.

## Repository structure

```
open-world-category-discovery/
├── README.md
├── requirements.txt
└── experiments/
    ├── day01_kmeans.ipynb
    └── figures/
        ├── kmeans_k3.png
        └── kmeans_k4.png
```
