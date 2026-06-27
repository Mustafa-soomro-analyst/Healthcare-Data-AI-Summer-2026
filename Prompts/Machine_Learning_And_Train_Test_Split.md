# Day 10: Machine Learning & Train/Test Splits
**Date:** June 2026  
**Objective:** Split cleaned clinical data into training and testing sets to prevent model cheating,
train a Random Forest algorithm, and generate a stakeholder report.

---
## Section 1: The Data Split (80/20 Rule)
**Goal:** Separate the features (`X`) from the target diagnosis (`y`), 
and split the 303 patient records into a study guide and a final exam.

### Execution Script:
```python
import pandas as pd
from sklearn.model_selection import train_test_split

fallback_url = "[https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv)"
df = pd.read_csv(fallback_url)

# Separate Clues (X) from Diagnosis (y)
X = df.drop('target', axis=1) 
y = df['target']

# 80/20 Split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

print(f"Total Patients in original database: {len(df)}")
print(f"Patients reserved for AI Training: {len(X_train)}")
print(f"Patients reserved for AI Testing: {len(X_test)}")

Verified Metrics:
Total Patients: 303
Training Set Size: 242
Testing Set Size: 61

Section 2: Training the Random Forest Classifier
Goal: Train the AI on the 242 records and test its diagnostic accuracy on the hidden 61 records.

Execution Script:
Python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# Initialize and Train
model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)

# Predict and Grade
predictions = model.predict(X_test)
accuracy = accuracy_score(y_test, predictions)

print(f"Model Accuracy on Hidden Data: {accuracy * 100:.2f}%")

Section 3: Stakeholder Reporting Prompt
Task: Translate raw accuracy metrics into a professional summary for the hospital board.

System Prompt:
Plaintext
You are a Lead Clinical Data Scientist reporting to the hospital board. 

[MODEL EVALUATION METRICS]
- Algorithm: Random Forest Classifier
- Training Set: 242 patient records
- Testing Set (Hidden): 61 patient records
- Final Accuracy Score: [INSERT YOUR PERCENTAGE HERE]

Write a brief, 3-sentence executive summary explaining the model's performance on the hidden testing data.
Frame the accuracy score as a measure of diagnostic reliability, but include a standard disclaimer that AI should assist,
not replace, physician judgment. 
AI Generated Stakeholder Report:
The Random Forest classifier was evaluated on a hidden testing set of **61 patient records** and achieved a final accuracy of
83.61%, indicating its overall diagnostic reliability in correctly classifying previously unseen cases.
This performance suggests that the model has strong potential to support clinical decision-making by providing consistent predictions on new patient data,
subject to the limitations of the evaluation dataset. However, the model is intended to assist clinicians rather than replace physician judgment,
and all AI-generated recommendations should be interpreted alongside clinical expertise and patient-specific findings.``



