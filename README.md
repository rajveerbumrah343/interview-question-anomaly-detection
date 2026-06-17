# interview-question-anomaly-detection

Q1
What is anomaly detection?
▾
Concept
Anomaly detection is the process of identifying data points, events, or observations that deviate significantly from the expected pattern or normal behavior in a dataset. These unusual data points are called anomalies, outliers, or novelties.

Think of it like a security guard who knows what "normal" looks like and raises an alarm when something unusual appears. The goal is to separate the rare, unusual events from the majority of normal data.

💡 Interview tip: Say: 'It's about finding the needle in a haystack — identifying rare events that don't conform to expected patterns.'
Q2
What are the main types of anomalies in data?
▾
Concept
There are three main types:

1. Point anomalies — A single data point that is far from the rest. Example: a single transaction of ₹1,00,000 in a history of ₹500 transactions.

2. Contextual anomalies — A data point is anomalous in a specific context but not globally. Example: 35°C temperature is normal in summer but anomalous in winter.

3. Collective anomalies — A collection of related data points that are anomalous together, though individual points may seem normal. Example: a sudden spike pattern in network traffic for 10 minutes.

💡 Interview tip: Always give examples for each type — interviewers love when you connect theory to real scenarios.
Q3
How does anomaly detection differ from noise removal?
▾
Concept
Anomaly detection is about finding meaningful, informative deviations that may indicate fraud, failure, or rare events. These outliers are important and need to be flagged and investigated.

Noise removal is about eliminating random, meaningless variations in data (sensor errors, measurement imprecision) that don't carry useful information.

The key difference: anomalies are meaningful deviations we want to study; noise is meaningless variation we want to discard. Removing an anomaly would destroy valuable signal.

💡 Interview tip: A common interview trap — emphasize that anomalies have business value and should NOT be removed, unlike noise.
Q4
Explain outliers and their impact on datasets.
▾
Concept
Outliers are observations that lie an abnormal distance from other values. Their impact:

• Statistical measures: Mean and standard deviation are heavily skewed. A single extreme value can shift the mean significantly.
• Model performance: Linear regression coefficients get pulled toward outliers, reducing accuracy.
• Visualization: Outliers compress the scale of plots, hiding patterns in the majority of data.
• Machine learning: Many algorithms (k-NN, k-Means) are distance-based and outliers distort distance calculations.

However, in fraud detection or medical diagnosis, the outlier IS the target — so context matters greatly.

💡 Interview tip: Always mention both the harm (distortion) AND the value (signal in fraud/medical contexts).
Q5
Supervised vs unsupervised anomaly detection?
▾
Concept
Supervised: Requires labeled data (normal vs anomaly). Train a classifier on both classes. Examples: SVM, Random Forest. Pros: high accuracy. Cons: labeling anomalies is expensive and rare anomalies cause class imbalance.

Unsupervised: No labels needed. Assumes anomalies are rare and different from normal data. Examples: Isolation Forest, LOF, DBSCAN. Pros: no labeling cost, discovers unknown anomalies. Cons: higher false positive rate.

Semi-supervised: Trained only on normal data, anything deviating is flagged. Examples: Autoencoders, One-Class SVM. Best balance in practice.

💡 Interview tip: For freshers, mentioning semi-supervised shows depth — most real-world systems use this approach.
Q6
Real-world applications of anomaly detection?
▾
Concept
• Finance: Credit card fraud detection, money laundering detection
• Cybersecurity: Intrusion detection, DDoS attack identification
• Healthcare: Detecting abnormal ECG patterns, rare disease diagnosis
• Manufacturing: Predictive maintenance — detecting equipment faults before failure
• E-commerce: Fake review detection, bot traffic identification
• IT Operations: Server/cloud resource utilization monitoring
• Social Media: Trend anomalies, viral misinformation detection
• IoT/Sensors: Smart meter tampering detection

Q7
What is the role of statistics in anomaly detection?
▾
Concept
Statistics forms the mathematical backbone of anomaly detection:

• Z-score and standard deviation define how far a point is from the mean
• IQR (Interquartile Range) provides a robust outlier boundary
• Probability distributions (Gaussian, Poisson) model normal behavior
• Hypothesis testing (Grubbs test, chi-square) formally tests if a point is an outlier
• Bayesian methods update anomaly probability as new evidence arrives

Statistical methods are interpretable and computationally cheap, making them ideal baselines before trying complex ML models.

💡 Interview tip: Mention that statistical methods are your 'first line of defense' — shows engineering maturity.
Q8
How do you handle high-dimensional data in anomaly detection?
▾
Concept
High dimensions create the 'curse of dimensionality' — all points appear equidistant, making distance-based methods ineffective.

Solutions:
• Dimensionality reduction: Apply PCA or t-SNE first, then detect anomalies in lower-dimensional space
• Feature selection: Keep only the most informative features
• Subspace methods: Detect anomalies in random subspaces (used in Isolation Forest)
• Autoencoders: Neural networks that learn compact representations — high reconstruction error = anomaly
• Feature engineering: Create aggregate features that capture patterns across dimensions

💡 Interview tip: Isolation Forest and Autoencoders are the go-to answers for high-dimensional anomaly detection.
Q9
What preprocessing steps are important before anomaly detection?
▾
Concept
1. Handle missing values — impute or remove (missing itself may be an anomaly signal)
2. Normalize/standardize — Z-score or Min-Max scaling so features contribute equally
3. Remove true noise — sensor errors, data entry mistakes
4. Feature engineering — create time-based features (hour, day) for temporal data
5. Encode categoricals — one-hot or label encoding
6. Handle class imbalance — SMOTE, undersampling for supervised methods
7. Exploratory analysis — visualize distributions, understand normal behavior first

💡 Interview tip: Always mention that EDA (Exploratory Data Analysis) is the very first step — shows you think like a data scientist.
Q10
How do you select the threshold for flagging anomalies?
▾
Concept
Threshold selection depends on the business context and acceptable trade-offs:

• Statistical: Z-score > 3 (99.7% rule), or IQR × 1.5
• ROC curve: Plot TPR vs FPR, pick threshold based on business cost of false positives vs false negatives
• Precision-Recall curve: Better for imbalanced datasets
• Domain knowledge: A fraud team may prefer catching 95% of fraud (high recall) even with some false alarms
• Percentile-based: Flag top 1% of anomaly scores

There is no universal threshold — it must be calibrated to business requirements.

💡 Interview tip: Saying 'it depends on the cost of false positives vs false negatives' immediately shows practical thinking.
Q11
Explain the importance of feature selection in anomaly detection.
▾
Concept
Poor features = poor anomaly detection, regardless of algorithm sophistication.

• Reduces noise: Irrelevant features add dimensions that dilute the anomaly signal
• Speeds up computation: Fewer features = faster distance calculations
• Improves interpretability: Easier to explain why a point is flagged
• Reduces false positives: Anomaly in an irrelevant feature won't pollute results

Methods: Correlation analysis, mutual information, domain expert knowledge, PCA-based importance, LASSO regularization.

Q12
How to handle class imbalance in supervised anomaly detection?
▾
Concept
Class imbalance (e.g. 1% fraud, 99% normal) is the norm in anomaly detection.

• Oversampling: SMOTE — synthesize new minority (anomaly) samples
• Undersampling: Reduce majority class samples
• Class weights: Set class_weight='balanced' in sklearn — penalizes misclassifying minority more
• Anomaly-specific algorithms: Use Isolation Forest, One-Class SVM instead of standard classifiers
• Evaluation metric: Never use accuracy — use F1-score, AUC-ROC, or Average Precision instead

💡 Interview tip: Mentioning that 'accuracy is a misleading metric for imbalanced data' scores big points in interviews.
Q13
What metrics evaluate anomaly detection model performance?
▾
Concept
Since data is highly imbalanced, accuracy is useless. Use:

• Precision: Of all flagged anomalies, how many are real? (minimizes false alarms)
• Recall / Sensitivity: Of all real anomalies, how many did we catch? (minimizes missed threats)
• F1-Score: Harmonic mean of precision and recall
• AUC-ROC: Area under ROC curve — overall ranking ability
• Average Precision (AP): Better than AUC for highly imbalanced data
• False Positive Rate: Important when false alarms have high cost (e.g. surgery alerts)


Q14
What are common statistical methods for anomaly detection?
▾
Algorithm
• Z-Score method: Points beyond 3 standard deviations from mean are anomalies. Simple, fast, assumes Gaussian distribution.
• IQR method: Points below Q1−1.5×IQR or above Q3+1.5×IQR. Robust to non-Gaussian data.
• Grubbs test: Statistical test for single outlier in univariate data.
• Mahalanobis distance: Multivariate distance accounting for feature correlations — generalizes Z-score to multiple dimensions.
• Gaussian Mixture Models: Fit a mixture of Gaussians; low probability points are anomalies.

💡 Interview tip: For interviews, start with IQR and Z-score — they're simple, explainable, and often sufficient baselines.
Q15
Explain the Z-Score and its use in anomaly detection.
▾
Algorithm
Z-Score measures how many standard deviations a data point is from the mean:

Z = (x − μ) / σ

Where μ = mean, σ = standard deviation.

In anomaly detection: if |Z| > 3, the point is an anomaly (falls outside 99.7% of the distribution under Gaussian assumption).

Example: Transaction amount mean = ₹500, σ = ₹100. A transaction of ₹1200 has Z = (1200−500)/100 = 7.0 → clear anomaly.

Limitation: Sensitive to outliers itself — one extreme value shifts mean and σ, potentially hiding other anomalies.

💡 Interview tip: Always mention the limitation: Z-score is itself influenced by outliers, so IQR or robust statistics are preferred.
Q16
How does k-NN work for anomaly detection?
▾
Algorithm
k-NN anomaly detection works on a simple intuition: normal points have similar neighbors; anomalies don't.

Algorithm:
1. For each data point, find its k nearest neighbors
2. Compute the anomaly score = distance to kth nearest neighbor (or average distance to k neighbors)
3. Points with high scores (far from their neighbors) are anomalies

Threshold: Set a percentile cutoff (e.g., top 5% highest scores = anomaly).

Pros: No assumptions about data distribution, works well in low dimensions.
Cons: O(n²) computation, sensitive to k value, poor in high dimensions.

💡 Interview tip: Explain why it fails in high dimensions (curse of dimensionality) — interviewers love when you know the limitations.
Q17
How can cluster analysis detect anomalies?
▾
Algorithm
Clusters group similar data points. Anomalies either:
1. Don't belong to any cluster (fall outside all clusters)
2. Belong to very small, sparse clusters
3. Are far from their assigned cluster center

K-Means approach: Compute distance from each point to its cluster centroid. Points with distance above a threshold are anomalies.

DBSCAN approach: Directly labels points as "core", "border", or "noise" — noise points are anomalies.

Limitation of K-Means: You must predefine k and it assumes spherical clusters. DBSCAN is more robust for anomaly detection.

Q18
How does the Isolation Forest algorithm work?
▾
Algorithm
Isolation Forest exploits a key insight: anomalies are few and different, so they're easier to isolate.

Algorithm:
1. Build random binary trees by randomly selecting a feature and a random split value
2. Repeat to build a forest of such trees
3. Anomaly score = average path length to isolate a point across all trees

Anomalies require fewer splits to isolate (shorter path) because they're in sparse regions. Normal points need many splits (longer path).

Formula: score = 2^(−avg_path_length / c(n)) where c(n) normalizes by expected path in a random BST.

Pros: Fast (O(n log n)), handles high dimensions, no distance computation needed, works well on large datasets.

💡 Interview tip: Isolation Forest is the most popular answer in data science interviews — memorize the core intuition: 'anomalies are easier to isolate.'
Q19
Explain LOF — Local Outlier Factor.
▾
Algorithm
LOF measures local density deviation of a point relative to its neighbors. A point is anomalous if its local density is much lower than its neighbors'.

Steps:
1. Compute reachability distance between points
2. Calculate Local Reachability Density (LRD) = inverse of average reachability distance
3. LOF score = average ratio of neighbors' LRD to point's own LRD

LOF score ≈ 1 → normal point. LOF >> 1 → anomaly (surrounded by much denser neighbors).

Key advantage: LOF is local — it handles datasets where different regions have different densities, unlike global methods like Z-score.

💡 Interview tip: LOF shines when you say 'it detects anomalies relative to their local neighborhood, not the global distribution.'
Q20
How does DBSCAN detect anomalies?
▾
Algorithm
DBSCAN (Density-Based Spatial Clustering of Applications with Noise) classifies points as:
• Core points: Has ≥ minPts neighbors within radius ε
• Border points: Within ε of a core point but fewer than minPts neighbors
• Noise points: Neither core nor border → these are anomalies

DBSCAN directly outputs anomaly labels without requiring k clusters to be specified.

Params to tune: ε (neighborhood radius) and minPts (minimum points). Use k-distance plot to select ε.

Advantage: Finds arbitrary-shaped clusters and naturally identifies outliers without assumptions.

Q21
Explain One-Class SVM for anomaly detection.
▾
Algorithm
One-Class SVM is a semi-supervised method trained only on normal data. It learns a decision boundary that encloses normal data in a high-dimensional feature space.

Idea: Find the smallest hypersphere (or hyperplane from origin) that contains most normal training points. At inference, points outside this boundary = anomalies.

Key parameter: ν (nu) — controls the fraction of training data allowed to be outside the boundary (= expected anomaly rate).

Kernel trick: RBF kernel maps data to infinite-dimensional space, enabling non-linear boundaries.

Pros: No anomaly labels needed. Cons: Slow on large datasets, sensitive to ν.

💡 Interview tip: One-Class SVM = 'draw a tight fence around normal data, flag anything outside.'
Q22
How do autoencoders detect anomalies?
▾
Algorithm
An autoencoder is a neural network that learns to compress data and reconstruct it:

Input → Encoder → Bottleneck (latent space) → Decoder → Reconstructed output

Training: Train only on normal data. The network learns a compressed representation of normalcy.

Detection: At test time, compute reconstruction error = MSE(input, reconstruction). Normal data → low error. Anomalies → high error (the network can't reconstruct patterns it never learned).

Threshold: Set a reconstruction error cutoff (e.g., 95th percentile of training error).

Best for: Image anomaly detection, high-dimensional tabular data, time-series.

💡 Interview tip: The key phrase: 'the autoencoder memorizes normalcy — it fails to reconstruct anomalies, revealing them through high reconstruction error.'
Q23
How does PCA help identify anomalies?
▾
Algorithm
PCA reduces data to principal components capturing maximum variance.

Anomaly detection approach:
1. Fit PCA on normal training data
2. For a new point: project it onto principal components, then reconstruct it back
3. Compute reconstruction error = distance between original and reconstructed point
4. High reconstruction error → anomaly (the point doesn't fit the normal subspace)

Alternatively: anomalies often have large values in the minor (low-variance) components, which normal data rarely activates.

Advantage: Computationally cheap, interpretable, handles correlated features well.

Q24
Gaussian Mixture Models: benefits and drawbacks for anomaly detection?
▾
Algorithm
GMM fits a mixture of k Gaussian distributions to data. Points with very low probability density are anomalies.

Benefits:
• Models multi-modal distributions (data with multiple natural clusters)
• Provides probabilistic scores — easy to threshold
• Can capture correlations between features
• Works well when data clusters are roughly Gaussian

Drawbacks:
• Must specify number of components k
• Sensitive to initialization
• Assumes Gaussian-shaped clusters — fails with irregular shapes
• Computationally expensive in high dimensions
• Can be fooled if anomalies cluster together

Q25
How does Support Vector Machine (SVM) adapt for anomaly detection?
▾
Algorithm
Standard SVM is binary classification. For anomaly detection:

One-Class SVM: Trained on normal data only. Learns a boundary in high-dimensional space beyond which points are anomalies (as covered in Q21).

Two-Class SVM: If some labeled anomalies exist, train a binary SVM with normal vs anomaly. Use class weights to handle imbalance.

SVDD (Support Vector Data Description): A variation that finds the minimum enclosing hypersphere around normal data. Anomalies fall outside this sphere.

Q26
How does Random Cut Forest detect anomalies?
▾
Algorithm
Random Cut Forest (RCF) — developed by Amazon for AWS — is designed for streaming/real-time anomaly detection.

Algorithm:
1. Build a forest of random cut trees on streaming data windows
2. For each new point, compute its Collusive Displacement — how much does adding/removing this point change the structure of the trees?
3. High displacement = anomalous point

Key advantage over Isolation Forest: RCF updates incrementally — it doesn't need to retrain on new data, making it ideal for real-time streaming scenarios.

Used in Amazon Kinesis Data Analytics for real-time monitoring.

💡 Interview tip: Mention RCF when asked about streaming or real-time anomaly detection — shows awareness of production systems.
Q27
Explain time-series anomaly detection and its unique challenges.
▾
Algorithm
Time-series data has temporal ordering, meaning observations are correlated across time. This creates unique challenges:

Unique challenges:
• Seasonality: A value that's normal in July may be anomalous in January
• Trend: Rising baselines mean old thresholds become invalid
• Autocorrelation: Consecutive observations aren't independent
• Concept drift: Normal behavior evolves over time
• Lag effects: Anomalies may have delayed impact

Methods: ARIMA residual analysis, STL decomposition + outlier detection on residuals, LSTM autoencoders, Prophet + anomaly scoring.
