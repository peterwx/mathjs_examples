# Index

${toc}

# Confusion matrix

A Confusion Matrix is a tabular layout used to describe the performance of a classification model. From it, we extract core metrics like Accuracy, Precision, Recall, and the F1-Score.
- What it means: It cross-references actual classes against predicted classes. For a binary scenario, it maps True Positives (TP), False Positives (FP), False Negatives (FN), and True Negatives (TN).
- What it's used for: Evaluating classification models beyond simple accuracy, especially when dealing with imbalanced datasets.

++Math.js Implementation++
Assuming we have a confusion matrix structured as:

$M = \begin{bmatrix} TP & FP \\ FN & TN \end{bmatrix}$

```math
# Define the confusion matrix directly
M = [[45, 5], [8, 92]]

# Extract elements using 1-based indexing
tp = M[1, 1]
fp = M[1, 2]
fn = M[2, 1]
tn = M[2, 2]

# Calculate metrics
accuracy = (tp + tn) / sum(M)
precision = tp / (tp + fp)
recall = tp / (tp + fn)
f1Score = 2 * (precision * recall) / (precision + recall)
```

When evaluating classification models, relying solely on "Accuracy" can be highly misleading—especially if your data is imbalanced (e.g., a rare disease that only affects 1% of patients).
Here is what the core metrics derived from the matrix actually mean, how they behave, and when to prioritize them:
## 1. Accuracy

The Formula: $\frac{TP + TN}{TP + TN + FP + FN}$
- What it means: The proportion of total predictions (both positive and negative) that the model got exactly right.
- When to use it: Only when your target classes are well-balanced in the dataset.
- The Trap: If 95% of your data is "Not Fraud", a broken model that predicts "Not Fraud" 100% of the time will boast a 95% accuracy while being completely useless at detecting fraud.

## 2. Precision (Positive Predictive Value)

The Formula: $\frac{TP}{TP + FP}$
- What it means: "Out of all the targets the model claimed were positive, how many were actually positive?" It is a measure of quality, focusing heavily on minimizing False Positives.
- When to use it: When the cost of a False Positive is incredibly high. For example, a spam filter. If a legitimate email (False Positive) is flagged as spam, you might miss an important business message. You want high precision so that when something is flagged as spam, you are certain it is.

## 3. Recall (Sensitivity / True Positive Rate)

The Formula: $\frac{TP}{TP + FN}$
- What it means: "Out of all the actual positive targets in the real world, how many did the model manage to find?" It is a measure of quantity/coverage, focusing heavily on minimizing False Negatives.
- When to use it: When the cost of a False Negative is catastrophic. For example, medical screening or cancer detection. If a patient has cancer but the model says they don't (False Negative), they miss life-saving treatment. It is much better to have a few false alarms (False Positives) that get cleared up later by secondary testing.

## 4. F1-Score

The Formula: $2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$
- What it means: The harmonic mean of Precision and Recall. It balances both metrics into a single score. Unlike an arithmetic average, the harmonic mean penalizes extreme imbalances (if Precision is 1.0 but Recall is 0.0, the F1-score drops to 0, not 0.5).
- When to use it: When you need a reliable baseline metric for an imbalanced dataset and you care equally about minimizing both False Positives and False Negatives.

Summary Checklist

| Metric    | Primary Focus                   | Best Used For...                                     |
| :-------: | :-----------------------------: | :--------------------------------------------------: |
| Accuracy  | Overall correctness             | Balanced datasets.                                   |
| Precision | Minimizing False Positives (FP) | Spam filters, ad targeting, legal sentencing.        |
| Recall    | Minimizing False Negatives (FN) | Medical diagnoses, fraud detection, security alarms. |
| F1-Score  | Balance between both errors     | General performance on uneven/imbalanced data.       |
