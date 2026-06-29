# Day 11: Confusion Matrix & Clinical Risk Assessment
**Date:** June 2026  
**Objective:** Deconstruct the "Accuracy" metric by generating a Confusion Matrix to analyze False Negatives and False Positives in a medical AI model.

---

## Section 1: Generating the Confusion Matrix
* **Goal:** Force the Random Forest model to display its exact mistakes on the 61-patient testing set.

### Execution Script:
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Load and Split Data
fallback_url = "[https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv)"
df = pd.read_csv(fallback_url)
X = df.drop('target', axis=1) 
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

# Train and Predict
model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)
predictions = model.predict(X_test)

# Map numeric outcomes to text for readability
y_test_words = y_test.replace({0: 'Healthy', 1: 'Heart Disease'})
predictions_words = pd.Series(predictions).replace({0: 'Healthy', 1: 'Heart Disease'})

# Generate Confusion Matrix
conf_matrix = pd.crosstab(y_test_words.values, predictions_words.values, 
                          rownames=['Actual Truth'], 
                          colnames=['AI Prediction'])
print(conf_matrix)

Verified Metrics:
True Positives (Caught the disease): 27

True Negatives (Correctly identified healthy): 24

False Positives (False alarms): 5

False Negatives (Missed the disease - FATAL): 5

Section 2: Clinical Risk Report
Task: Generate a C-Suite level risk assessment explaining why optimizing to reduce False Negatives is critical for patient safety.

AI Generated Stakeholder Report:
Model Strength: The AI correctly identified 27 patients with heart disease (True Positives), demonstrating a strong ability to detect patients
who may require further clinical evaluation and timely intervention.

Clinical Risk: The 5 False Negative cases are a significant patient safety concern because the model failed to identify patients who actually had heart disease.
Such errors may contribute to delayed diagnosis or missed opportunities for further assessment if AI output is used without appropriate clinical oversight,
 making false negatives particularly important to minimize in many healthcare screening applications.

Recommendation: Consider evaluating a decision threshold that increases the model's sensitivity (recall) to reduce the number of false negatives, while recognizing that this will likely increase the number of false positives and may require additional follow-up testing. Any threshold adjustment should be validated on independent data and used as a decision-support tool alongside physician judgment rather than as a standalone diagnostic system.
