# Day 12: Explainable AI (XAI) & Feature Importance
**Date:** June 2026  
**Objective:** Extract internal decision weights from a Random Forest model to solve
the "Black Box" problem and translate the findings into actionable clinical insights.

---

## Section 1: Extracting the AI's Brain
* **Goal:** Identify which clinical clues the AI relied on the most to predict heart disease.

### Execution Script:
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Load Data & Train Model
fallback_url = "[https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv]
(https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv)"
df = pd.read_csv(fallback_url)
X = df.drop('target', axis=1) 
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

model = RandomForestClassifier(random_state=42)
model.fit(X_train, y_train)

# Extract Feature Importances
importances = model.feature_importances_
feature_ranking = pd.DataFrame({
    'Medical_Clue': X.columns,
    'Importance_Percentage': importances * 100
})

feature_ranking = feature_ranking.sort_values(by='Importance_Percentage', ascending=False).reset_index(drop=True)
print(feature_ranking.head(5))
Verified Metrics:
#1 Diagnostic Clue: oldpeak (ST depression induced by exercise relative to rest)

Decision Weight: 12.85%

Section 2: Clinical Translation Brief
Task: Translate the raw mathematical feature weight into a professional briefing for the Head of Cardiology.

AI Generated Stakeholder Report:
The Random Forest model identified oldpeak (ST depression induced by exercise relative to rest) as its most influential predictive feature,
contributing 12.85% of the model's overall decision-making weight. This indicates that, among the variables available to the model,
exercise-induced ST-segment depression consistently provided the greatest predictive value for distinguishing patients at higher risk of heart disease.
From a clinical perspective, this aligns with established cardiology practice, as ST-segment depression during exercise testing is a recognized indicator of myocardial ischemia
and may reflect underlying coronary artery disease.

Given this finding, the cardiology department may consider ensuring that exercise stress-test data and associated ECG measurements are collected consistently and documented with
high quality whenever clinically appropriate. Particular attention should be paid to standardized acquisition, interpretation,
and recording of stress-test parameters so that both clinicians and AI-assisted decision-support systems have reliable input data.
