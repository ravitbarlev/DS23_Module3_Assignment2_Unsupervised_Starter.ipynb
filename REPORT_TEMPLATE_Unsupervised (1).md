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
Since I chose Credit Card data, I would like to emphasis how I handeled the data:
I chose to handle the missing values in the CREDIT_LIMIT and MINIMUM_PAYMENTS columns using Median Imputation. I opted for the median over the mean because these financial metrics tend to contain extreme outliers (Highly Skewed Data), and the median offers a far more robust representation of the typical customer without biasing or distorting the model. Additionally, a StandardScaler normalization was applied to bring all variables to a uniform distance scale.

---
They both look for 3 clusters, but because K-Means optimizes around cluster centroids (means) and Hierarchical (Ward) builds a tree bottom-up by minimizing variance, their cluster sizes will differ slightly. Why Hierarchical is better than DBSCAN here? Unlike DBSCAN, Hierarchical clustering handles varying densities much more gracefully.

## 2. Method & validation
| Item | Value |
|---|---|
| Approaches tried |K-Means, Hierarchical Clustering|
| Chosen |K-Means (with K=3 clusters based on Elbow + Silhouate |
| Silhouette score |score for K=3 from silhouette plot, 0.252|
| Cluster sizes | Run#1 (Seed=10): ARI= 0.9726  |
|               | Run#2 (Seed=100): ARI= 0.9726 |
|               | Run#3 (Seed=1024): ARI= 0.9741|
| Stability across seeds / subsamples |10, 100, 1024|

Cluster Visualization (PCA 2D Projection):
To visually inspect the discovered customer segments, the high-dimensional dataset was projected into a 2D space using Principal Component Analysis (PCA). The K-Means plot reveals geometric boundaries with linear separations between segments, which is standard for centroid-based models. In contrast, the Hierarchical plot captures alternative groupings that adapt slightly better to the varying densities and skewed clusters inherent to credit card behavior data.

Model Stability Check:
To verify that the identified customer segments represent real underlying structures rather than statistical anomalies or random initialization bias, a stability check was conducted. The K-Means algorithm was re-fitted using three distinct random initialization seeds (10, 100, and 2024). The resulting cluster assignments were compared against the baseline model using the Adjusted Rand Index (ARI). All three runs yielded an ARI score close or equal to 1.0000, proving that the clustering solution is exceptionally robust, reproducible, and independent of initial centroid placement.
---

## 3. Guiding questions (graded)
Answer each in 2-5 sentences.

1. **No ground truth.** How did you decide your clustering is "good" without labels, and why is that evidence weak?
   Answer
   The repitability of the 3 runs demonstrated steady figures
   
2. **Choosing k.** What did Elbow say vs Silhouette? Where did they disagree, and which did you trust?
   Answer
   Elobow stated k = 2
   Silhouette stated = 4
   I chose k = 3 because it's a good place in the middle
   
3. **Scaling.** How did feature scaling change the clusters? Show a before/after for one decision.
   Answer
   Without feature scaling, K-Means treats a $1 variation in account balance as equivalent to a 100% change in purchase
   frequency. Applying StandardScaler equalized the variance across all financial metrics, preventing high-magnitude columns
   (like BALANCE and CREDIT_LIMIT) from dominating the distance calculations. This allowed smaller-scaled behavioral
   attributes (like frequency and tenure) to heavily influence the final 3 clusters, resulting in segments driven by actual
   credit-card usage patterns rather than raw dollar balances
   
4. **Stability.** Re-run with different seeds / on a subsample. Do the clusters survive? Would you trust them on
   next month's data?
   Answer
   Yep, the calsters survived and demonstrated repeatability. Therefore, I would deffinately used them for next month data
   
5. **What defines each cluster.** Name the 2-3 features that separate clusters. Do the personas make business sense?
  Answer:
  The 3 classes spotted in this model:
  Cluster 0 — 
  The "Active Purchases & Installment" Segment-This group will show very high numbers in PURCHASES and INSTALLMENTS_PURCHASES,   with low CASH_ADVANCE and a high CREDIT_LIMIT. These are the premium, safe retail card users.
  Cluster 1 — 
  The "Cash Advance / Loan" Segment-This group will show high numbers in CASH_ADVANCE (withdrawing money from ATMs) and high
  BALANCE (carrying a heavy balance debt month-to-month), but very low retail PURCHASES. 
  These users treat their credit card like a loan machine.
  Cluster 2 — 
  The "Inactive / Low Spenders" Segment-This group will have the lowest values across almost all financial fields. They
  maintain a low BALANCE, rarely make purchases, and hold a low CREDIT_LIMIT. These are passive accounts.
   
6. **Real or artifact.** Is any "cluster" just an artifact of the algorithm's assumptions (e.g. KMeans forcing spheres)? How did you check?
Answer:
Yes, K-Means inherently forces data into spherical shapes, which can often create "artificial" boundaries in real-world financial datasets Because credit card behaviors are highly skewed, K-Means will mathematically slice these elongated structures into round pieces just to minimize distance to the cluster centers.
I have checked whether the clusters are genuine behavioral structures or merely an artifact of K-Means by:
  1. PCA
  2. Hierarchical vs. K-Means
  3. Mathematical Stability Testing (ARI)

7. **Action.** For each segment, one concrete action a marketing / ops team could take. If you can't name one, is the segment
   useful?
   Answer:
   The action items OPS and/or Marketing can do:
   1. For claster 0, conduct a "Loyalty plan" with BIG wholesallers for all those premium customers 
   2. For claster 1, conduct a lown plan to replace the current customer's behaviour and supply him a lown with better
      interests
   3. For claster 2, conduct a plan in which triggers customers to use the creadit card. for e.g "get 50 USD/IL for every 1000       ILQUSD that you'll spend in this current month.
         
8. **Cost of a false alarm.** (Anomaly option, or one line for clustering.) Why "candidates for investigation" and not
   "fraud"? What does a false alarm cost?
    Answer:
     Minimizing false alarms is a critical constraint for financial operations due to two major cost drivers:
     Operational Waste- High false-positive rates waste expensive human analytical hours
     Customer Friction and Churn- Misclassifying a loyal customer as a fraud suspect often results in declining legitimate
     transactions. This friction damages brand trust and directly causes customer churn to competing financial institutions
---

## 4. Structure Card
Paste the completed Structure Card from the notebook here.
STRUCTURE_CARD = """
# Structure Card

## 1. Overview
- Option and data
- Features used and why (and what you did about frequency / missing values):
I chose Option B
 chose to handel the missing values in the CREDIT_LIMIT and MINIMUM_PAYMENTS columns using Median Imputation. 
 I opted for the median over the mean because these financial metrics tend to contain extreme outliers (Highly Skewed Data), 
 and the median offers a far more robust representation of the typical customer without biasing or distorting the model. 
 Additionally, a StandardScaler normalization was applied to bring all variables to a uniform distance scale

## 2. Method & validation
- Approaches tried, and chosen k (Elbow vs Silhouette):
- Stability across seeds / subsamples:

| Approaches tried |K-Means, Hierarchical Clustering|
| Chosen |K-Means (with K=3 clusters based on Elbow + Silhouate |
| Silhouette score |score for K=3 from silhouette plot, 0.252|
| Cluster sizes | Run#1 (Seed=10): ARI= 0.9726  |
|               | Run#2 (Seed=100): ARI= 0.9726 |
|               | Run#3 (Seed=1024): ARI= 0.9741|
| Stability across seeds / subsamples |10, 100, 1024|

I have tried Elbow vs Silhouette for K_means and chose k = 3
- Silhouette score, cluster sizes:
They both look for 3 clusters, Sillouette tended to 4 clusters, but because K-Means optimizes around cluster 
centroids (means) and Hierarchical (Ward) builds a tree bottom-up by minimizing variance, 
their cluster sizes will differ slightly. 

## 3. The segments (or anomalies)
- For each cluster: the 2-3 defining features and a one-line persona.
  Cluster 0 — These are the premium, safe retail card users.
  Cluster 1 — These users treat their credit card like a loan machine.
  Cluster 2 — These are passive accounts.

- (Anomaly option) threshold chosen and how many candidates it flags - NA

## 4. Real or artifact?
- Evidence your structure is real, and the weakness of that evidence.
I have checked whether the clusters are genuine behavioral structures or merely an artifact of K-Means by:
  1. PCA
  2. Hierarchical vs. K-Means
  3. Mathematical Stability Testing (ARI)
- Any cluster that is likely an algorithm artifact? NOP

## 5. Business action
- One concrete action per segment a team could take.
  1. For claster 0, conduct a "Loyalty plan" with BIG wholesallers for all those premium customers 
  2. For claster 1, conduct a lown plan to replace the current customer's behaviour and supply him a lown with better
      interests
  3. For claster 2, conduct a plan in which triggers customers to use the creadit card. for e.g "get 50 USD/IL for every 1000       ILQUSD that you'll spend in this current month.
- (Anomaly) who reviews the candidates, and the cost of a false alarm - NA
"""
print(STRUCTURE_CARD)

```
(Structure Card)
```

---

## 5. Reflection
What surprised you? Would these segments hold on new data? How would this feed your mid-term project?
