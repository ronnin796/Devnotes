#flashcards #review #MLmodels
## what is clustering?
- Unsupervised Learning
- Grouping of Data points
- Same group have same features and vice versa
- used when we have features but not label
## Basic Algorithm for K-means
- 
```
function KMeans(X, K, max_iters = 100, tol = 1e-4):
    Initialize centroids randomly from X

    for i in range(max_iters):
        # Assignment step
        Assign each data point to the nearest centroid

        # Update step
        For each cluster k:
            Update centroid[k] = mean of points assigned to cluster k

        # Check convergence
        If all centroid shifts < tol:
            break

    return centroids, labels

```
