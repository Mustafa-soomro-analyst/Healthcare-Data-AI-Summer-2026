## Day 13: Model Deployment & PicklingDate: July 2026Objective: Serialize and save a trained machine learning model into a portable file, and draft a deployment handoff ticket for software engineering teams.
# Section 1: Freezing the AI (Pickling)Goal: Use the joblib library to export the trained Random Forest model's "brain" into a file that can be loaded on any server.Execution Script:import pandas as pd
import joblib
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Load Data & Train Model
fallback_url = "[https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv](https://raw.githubusercontent.com/mrdbourke/zero-to-mastery-ml/master/data/heart-disease.csv)"
df = pd.read_csv(fallback_url)
X = df.drop('target', axis=1) 
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

ai_model = RandomForestClassifier(random_state=42)
ai_model.fit(X_train, y_train)

# --- DEPLOYMENT LOGIC ---

# 1. Save the Model
filename = 'heart_disease_ai_v1.joblib'
joblib.dump(ai_model, filename)
print(f"SUCCESS: Model saved to disk as '{filename}'")

# 2. Wipe from Memory
del ai_model 

# 3. Load the Model back from the file
deployed_ai = joblib.load(filename)
print("SUCCESS: Model loaded back into memory from disk.")

# 4. Test on a hidden patient
patient_zero = X_test.iloc[[0]]
prediction = deployed_ai.predict(patient_zero)

if prediction[0] == 1:
    print("The loaded AI predicts: HEART DISEASE")
else:
    print("The loaded AI predicts: HEALTHY")
Verified Metrics:
Deployment Status: Successfully saved to heart_disease_ai_v1.joblib.
Patient Zero Prediction: HEALTHY (Model successfully re-initialized from disk)
# Section 2: Software Engineering Handoff TicketTask:
Draft a professional Jira ticket instructing frontend developers on how to implement the model into a web application.
AI Generated Jira Ticket:Title: Deploy heart_disease_ai_v1.joblib for Heart Disease Prediction Web ApplicationSummary:
The attached file, heart_disease_ai_v1.joblib, contains a trained Random Forest Classifier for binary heart disease prediction.
This model is intended to serve as the backend inference engine for the hospital's web application.Implementation Instructions:Load the model using the Python joblib library:import joblib
model = joblib.load("heart_disease_ai_v1.joblib")
When a user submits the prediction form, collect the required clinical inputs, arrange them in the same feature order used during model training,
and pass them to the model as a 2-dimensional array with shape (1, 13), where one row represents a single patient and the 13 columns represent the required numerical clinical features
(e.g., Age, Blood Pressure, Cholesterol, etc.).
Expected Input:Shape: (1, 13)
Data Type: Numeric values onlyFeature Order: Must exactly match the order used during model training.
Expected Output:A single binary prediction:0 = Healthy,1 = Heart Disease
The web application's submit action should invoke the model's prediction method using the validated input array and display the returned binary classification to the user in the application's results interface.
