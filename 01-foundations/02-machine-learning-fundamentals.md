# Chapter 2 – Machine Learning Fundamentals (Simplified)

## Learning Objectives
By the end of this chapter, you should be able to:
- Explain how ML problems differ from conventional software problems.
- Distinguish supervised, unsupervised, semi-supervised, and reinforcement learning.
- Frame business questions as classification, regression, ranking, anomaly detection, clustering, or forecasting.
- Understand examples, labels, features, parameters, loss functions, and optimization.
- Create train/validation/test splits safely without leakage.
- Select evaluation metrics that reflect real-world error costs.
- Recognize underfitting, overfitting, class imbalance, drift, and distribution shift.
- Explain how ML models complement LLMs and agents.
- Design a production lifecycle with monitoring, retraining, and human review.

---

## 1. Why Machine Learning Exists
Conventional software works well when rules are clear.  
Example: validating a date, calculating tax, or rejecting unauthorized actions.  

But some problems are different:  
- Fraud detection  
- Customer churn prediction  
- Delivery time estimation  
- Image defect classification  
- Ranking search results  
- Escalating support tickets  

Writing rules for these is brittle and incomplete.  
**Machine learning learns patterns from historical examples and applies them to new cases.**

---

## 2. Core Vocabulary
- **Example (observation):** One record used for learning or evaluation (ticket, customer, image, transaction).  
- **Feature:** Input variable (e.g., affected users, outage indicator, customer tier).  
- **Label (target):** Desired outcome (fraud/not fraud, escalation yes/no).  
- **Model:** Function mapping features → prediction. Contains parameters learned during training.  
- **Training:** Adjusting parameters to match known outcomes.  
- **Inference:** Using the trained model on new data.  
- **Loss function:** Converts prediction error into a number to minimize.  
- **Metric:** Measures performance for evaluation/monitoring.  

---

## 3. Learning Paradigms
### 3.1 Supervised Learning
Uses examples with known outcomes.  
Tasks: classification, regression, ranking, forecasting.  

- **Classification:** Predicts categories (urgent vs non-urgent). Often outputs probabilities.  
- **Regression:** Predicts continuous values (delivery time, demand).  
- **Ranking:** Orders candidates by relevance (search results, recommendations).  
- **Forecasting:** Predicts future values using time-based data (weekly demand, system load).  

### 3.2 Unsupervised Learning
No labels; discovers structure.  
Tasks: clustering, dimensionality reduction, anomaly detection.  

### 3.3 Semi-Supervised Learning
Mix of small labeled + large unlabeled data. Useful when labeling is expensive.  

### 3.4 Self-Supervised Learning
Creates labels from the data itself (e.g., predicting missing words in text).  

### 3.5 Reinforcement Learning
Agent interacts with environment, learns by rewards/penalties. Useful when decisions affect future states.  

---

## 4. Framing the Business Problem
Many ML failures start with vague goals.  
Better approach:  
- Define the decision to improve.  
- Convert into a target (e.g., escalation within 30 minutes).  
- Define unit of prediction (ticket, customer, transaction).  
- Define prediction horizon (when outcome is measured).  
- Decide if ML is necessary — sometimes rules or small classifiers are enough.  

---

## 5. Data is Part of the Product
- **Data sources:** databases, logs, sensors, documents, annotations.  
- **Labels:** reflect policy, not pure truth (may encode bias or inconsistency).  
- **Feature availability:** must exist at prediction time (avoid leakage).  
- **Leakage patterns:** using future info, overlapping records, post-outcome notes.  
- **Data quality:** completeness, validity, timeliness, representativeness.  

---

## 6. Train, Validation, and Test Sets
- **Training:** learn parameters.  
- **Validation:** tune hyperparameters.  
- **Test:** estimate generalization.  

Splitting strategies:  
- Time-based (for forecasting).  
- Grouped (keep related records together).  
- Cross-validation (when data is limited).  

---

## 7. How Training Works
Steps:  
1. Predict with current parameters.  
2. Compare with known targets.  
3. Calculate loss.  
4. Adjust parameters.  

- **Parameters:** learned from data.  
- **Hyperparameters:** set by training process (learning rate, tree depth).  
- **Optimization:** find parameters that reduce loss (often gradient-based).  
- **Regularization:** prevent overfitting (limit complexity, dropout, early stopping).  

---

## 8. Generalization, Underfitting, and Overfitting
- **Underfitting:** model too simple, poor performance everywhere.  
- **Overfitting:** memorizes training data, fails on new data.  
- **Bias vs Variance:** trade-off between restrictive assumptions vs sensitivity to data.  
- **Learning curves:** show if more data or better features help.  

---

## 9. Evaluation Metrics
Metrics must match business needs.  

- **Confusion matrix:** TP, FP, TN, FN.  
- **Accuracy:** misleading for imbalanced data.  
- **Precision:** correctness of flagged cases.  
- **Recall:** coverage of true positives.  
- **F1 score:** balance of precision & recall.  
- **ROC-AUC & PR-AUC:** ranking quality; PR-AUC better for rare events.  
- **Calibration:** predicted probabilities match observed frequencies.  

---

## 10. Class Imbalance
When one class is much rarer than another (fraud vs non-fraud).  
Solutions:  
- Resampling (oversample minority, undersample majority).  
- Synthetic data (SMOTE).  
- Adjust thresholds.  
- Use metrics like PR-AUC instead of accuracy.  

---

## 11. Drift and Distribution Shift
Models assume training and production data are similar.  
- **Covariate shift:** input features change.  
- **Prior probability shift:** class balance changes.  
- **Concept drift:** relationship between features and labels changes.  
Detection: monitor distributions, metrics, and retrain when needed.  

---

## 12. Feature Engineering
Transform raw data into useful inputs.  
Examples:  
- Ratios, differences, aggregates.  
- Text embeddings.  
- Time-based features (lags, rolling averages).  
- Domain-specific encodings.  

---

## 13. Model Families
- **Linear models:** simple, interpretable.  
- **Decision trees & ensembles:** handle non-linearities, robust.  
- **Neural networks:** flexible, powerful, need more data.  
- **Nearest neighbors:** simple, memory-based.  
- **Probabilistic models:** capture uncertainty.  

---

## 14. Model Selection
Depends on:  
- Data size and quality.  
- Interpretability needs.  
- Latency and resource constraints.  
- Business risk tolerance.  

---

## 15. Production Lifecycle
- Training → Validation → Deployment → Monitoring → Retraining.  
- Monitor: accuracy, drift, latency, cost.  
- Retrain when performance drops.  
- Keep humans in review loop for critical tasks.  

---

## 16. Complementarity with LLMs
ML models handle structured predictions.  
LLMs handle unstructured text.  
Agents combine both:  
- ML classifier routes tickets.  
- LLM drafts response.  
- Agent orchestrates workflow.  

---

## 17. Common Failure Modes
- Data leakage.  
- Poor labeling.  
- Ignoring drift.  
- Wrong metric choice.  
- Overfitting.  
- Lack of monitoring.  

---

## 18. Human Oversight
Humans should:  
- Approve high-risk predictions.  
- Monitor dashboards.  
- Investigate anomalies.  
- Provide feedback for retraining.  

---

## 19. Mini Case Study
Example: Predicting ticket escalation.  
- Features: affected users, outage indicator, customer tier.  
- Label: escalation within 30 minutes.  
- Model: classifier.  
- Metric: recall (catch most urgent cases).  
- Oversight: human review for flagged tickets.  

---

## 20. Hands-on lab: build an escalation baseline

### Goal

Build a small classifier that estimates whether a support ticket should be escalated.

### Step 1: run the supplied example

```bash
python examples/02-machine-learning/ticket_priority_baseline.py
```

### Step 2: inspect the data

Identify:

- features;
- label;
- grouping variable;
- imbalance level;
- any suspicious leakage fields.

### Step 3: change the decision threshold

Compare:

- precision;
- recall;
- number of cases sent to human review.

### Step 4: add one feature

Examples:

- recent similar ticket count;
- customer tier;
- business-critical process indicator.

Explain whether the feature would truly be available at ticket creation time.

### Step 5: design a production policy

Specify:

- auto-escalation threshold;
- human-review interval;
- normal-routing threshold;
- fallback when the model is unavailable;
- monitoring metrics.

### Expected learning

The purpose of this lab is not to maximize a score. It is to connect problem framing, data splitting, metrics, thresholds, and operational policy.

---

## 21. Knowledge check

1. Why can a model with high accuracy be useless for a rare-event problem?
2. What is the difference between a parameter and a hyperparameter?
3. Give two examples of target leakage.
4. When should a time-based split be preferred over a random split?
5. What operational question does precision answer?
6. What operational question does recall answer?
7. Why should model thresholds be separated from model training?
8. What is the difference between data drift and concept drift?
9. Why can historical labels encode outdated policy?
10. How can a small classifier reduce LLM cost?

---

## 22. Interview questions

### Beginner

1. Explain supervised and unsupervised learning with one example each.
2. What is the purpose of a test set?
3. What is overfitting?
4. Why is accuracy insufficient for imbalanced classification?
5. What is the difference between training and inference?

### Intermediate

1. Design a split strategy for predicting equipment failure from repeated sensor readings per device.
2. How would you select a threshold for a fraud model?
3. Describe three leakage risks in a customer-churn dataset.
4. How would you evaluate a model when labels arrive 90 days later?
5. Explain how calibration differs from ranking quality.

### Senior

1. A model has stable offline metrics but declining business impact. How would you investigate?
2. Design a champion-challenger rollout for a critical support-routing model.
3. How would you monitor fairness and drift without exposing sensitive attributes broadly?
4. When would you choose rules, conventional ML, an LLM, or an agent for text-heavy ticket routing?
5. Describe a feedback loop that could bias future training data and how you would mitigate it.

### System design

Design an enterprise ticket-escalation platform that combines:

- deterministic severity policy;
- an ML risk score;
- LLM-based extraction from ticket text;
- active-incident lookup;
- human approval for critical escalation;
- full audit logging;
- drift monitoring and retraining.

Your design should address latency, failure modes, authorization, thresholding, data lineage, and safe fallback.

---

## 23. Chapter summary

Machine learning replaces some manually written decision logic with patterns learned from examples. The compact board sequence of data, training, 
