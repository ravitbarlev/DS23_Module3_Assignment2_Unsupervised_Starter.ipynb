# REPORT — Module 3 · Assignment 2 · Unsupervised Learning

**Name:** Ravit Bar-Lev **ID:** 029290400  **Date:** 11.07/26
**Chosen option:** B · Credit Card 

> Keep this report in English. There is no ground truth here, so "I argued it is good
> but the evidence is weak because ___" is a strong, honest answer.

---

## 1. Framing
Since I chose Credit Card data, I would like to emphasis that the new data was handeled:
"בחרתי לטפל בערכים החסרים בעמודות CREDIT_LIMIT ו-MINIMUM_PAYMENTS באמצעות מילוי ערכי החציון (Median Imputation) של אותן עמודות. בחרתי בחציון ולא בממוצע מכיוון שנתונים פיננסיים אלו נוטים להכיל ערכי קיצון גבוהים (Skewed Data), והחציון מייצג בצורה יציבה יותר את הלקוח הממוצע מבלי להטות את המודל. בנוסף, בוצע נרמול מסוג StandardScaler כדי להביא את כל המשתנים לסקאלה אחידה של מרחק."

What structure are you looking for, and what business decision does it serve?
In order to find the K-Means I used Elbow and Silhouate methods. Looking at the graphs (in which oresented in the notebook) It can be seen that
the Elbow Method and the Silhouette Score almost always disagree on the optimal number of clusters (K).The Silhouette Score usually peaks sharply 
at K = 2 (or sometimes K = 3). It strongly suggests that the data should only be split into two massive, distinct macro-segments (e.g., "Active Users" vs. "Inactive/Low-Spending Users").The Elbow Method usually shows a smooth, continuous decline with a very subtle, ambiguous "elbow" around K = 3,
K = 4, or even K = 5. It rarely shows a sharp bend at K = 2.

Distance / similarity measure chosen, and why:

Feature choices (and what you did about frequency / missing values):

---

## 2. Method & validation
| Item | Value |
|---|---|
| Approaches tried | |
| Chosen k (Elbow vs Silhouette) | |
| Silhouette score | |
| Cluster sizes | |
| Stability across seeds / subsamples | |

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
