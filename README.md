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
