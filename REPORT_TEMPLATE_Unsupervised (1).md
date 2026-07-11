# REPORT — Module 3 · Assignment 2 · Unsupervised Learning

**Name:** Ravit Bar-Lev **ID:** 029290400  **Date:** 11.07/26
**Chosen option:** B · Credit Card 

> Keep this report in English. There is no ground truth here, so "I argued it is good
> but the evidence is weak because ___" is a strong, honest answer.

---

## 1. Framing
What structure are you looking for, and what business decision does it serve?
Answer:
In order to find the K-Means I used Elbow and Silhouate methods. Looking at the graphs (in which oresented in the notebook) It can be seen that
the Elbow Method and the Silhouette Score almost always disagree on the optimal number of clusters (K).The Silhouette Score usually peaks sharply 
at K = 2 (or sometimes K = 3). It strongly suggests that the data should only be split into two massive, distinct macro-segments (e.g., "Active Users" vs. "Inactive/Low-Spending Users").The Elbow Method usually shows a smooth, continuous decline with a very subtle, ambiguous "elbow" around K = 3,
K = 4, or even K = 5. It rarely shows a sharp bend at K = 2.
To keep a long story short, I chose to continue with K_mean =3 because it captures actionable sub-behaviors while maintaining a reasonable Elbow drop

Distance / similarity measure chosen, and why:
Answer:
I chose Hierarchical Clustering (Agglomerative Clustering) because it's flexible in terms of claster shape. 
I also chose optimal number of clusters as K = 3. See above for enlightment.
I configurated both K-Means and Hierarchical Clustering to look for exactly 3 clusters. This makes it much cleaner to compare how the two different algorithms group the credit card customers.

Feature choices (and what you did about frequency / missing values):
Answer:
Since I chose Credit Card data, I would like to emphasis that the new data was handeled:
"בחרתי לטפל בערכים החסרים בעמודות CREDIT_LIMIT ו-MINIMUM_PAYMENTS באמצעות מילוי ערכי החציון (Median Imputation) של אותן עמודות. בחרתי בחציון ולא בממוצע מכיוון שנתונים פיננסיים אלו נוטים להכיל ערכי קיצון גבוהים (Skewed Data), והחציון מייצג בצורה יציבה יותר את הלקוח הממוצע מבלי להטות את המודל. בנוסף, בוצע נרמול מסוג StandardScaler כדי להביא את כל המשתנים לסקאלה אחידה של מרחק"
---
They both look for 3 clusters, but because K-Means optimizes around cluster centroids (means) and Hierarchical (Ward) builds a tree bottom-up by minimizing variance, their cluster sizes will differ slightly. Why Hierarchical is better than DBSCAN here? Unlike DBSCAN, Hierarchical clustering handles varying densities much more gracefully.

## 2. Method & validation
| Item | Value |
|---|---|
| Approaches tried |K-Means, Hierarchical Clustering|
| Chosen |K-Means (with K=3 clusters based on Elbow + Silhouate |
| Silhouette score |score for K=3 from silhouette plot, 0.252|
| Cluster sizes | Run#1 (Seed=10): ARI= 0.9726
                  Run#2 (Seed=100): ARI= 0.9726
                  Run#3 (Seed=1024): ARI= 0.9741|
| Stability across seeds / subsamples |10, 100, 1024|

Cluster Visualization (PCA 2D Projection):
To visually inspect the discovered customer segments, the high-dimensional dataset was projected into a 2D space using Principal Component Analysis (PCA). The K-Means plot reveals geometric boundaries with linear separations between segments, which is standard for centroid-based models. In contrast, the Hierarchical plot captures alternative groupings that adapt slightly better to the varying densities and skewed clusters inherent to credit card behavior data.

Model Stability Check:
To verify that the identified customer segments represent real underlying structures rather than statistical anomalies or random initialization bias, a stability check was conducted. The K-Means algorithm was re-fitted using three distinct random initialization seeds (10, 100, and 2024). The resulting cluster assignments were compared against the baseline model using the Adjusted Rand Index (ARI). All three runs yielded an ARI score close or equal to 1.0000, proving that the clustering solution is exceptionally robust, reproducible, and independent of initial centroid placement.

---

## 3. Guiding questions (graded)
Answer each in 2-5 sentences.

1. **No ground truth.** How did you decide your clustering is "good" without labels, and why is that evidence weak?
2. **Choosing k.** What did Elbow say vs Silhouette? Where did they disagree, and which did you trust?
3. **Scaling.** How did feature scaling change the clusters? Show a before/after for one decision.
4. **Stability.** Re-run with different seeds / on a subsample. Do the clusters survive? Would you trust them on next month's data?
5. **What defines each cluster.** Name the 2-3 features that separate clusters. Do the personas make business sense?
6. **Real or artifact.** Is any "cluster" just an artifact of the algorithm's assumptions (e.g. KMeans forcing spheres)? How did you check?
7. **Action.** For each segment, one concrete action a marketing / ops team could take. If you can't name one, is the segment useful?
8. **Cost of a false alarm.** (Anomaly option, or one line for clustering.) Why "candidates for investigation" and not "fraud"? What does a false alarm cost?

---

## 4. Structure Card
Paste the completed Structure Card from the notebook here.

```
(Structure Card)
```

---

## 5. Reflection
What surprised you? Would these segments hold on new data? How would this feed your mid-term project?
