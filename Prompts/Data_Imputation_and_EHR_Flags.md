# Project Mean vs. Median imputaion
# Goal: fill missing values using mean and medain imputaion
# Python Script
``import pandas as pd
import numpy as np

clinical_data = {
    'Patient_ID': [901, 902, 903, 904, 905],
    'Age': [45, 62, 29, 54, 38],
    'Heart_Rate': [72, np.nan, 68, 110, np.nan] # np.nan represents a missing blank cell
}

df_clinic = pd.DataFrame(clinical_data)

#data with missing values
print("--- Step#1: Clinical Data with Missing Values ---")
print(df_clinic)

#counting total missing values in each column
print("\n--- Step#2: Missing values per column")
print(df_clinic.isnull().sum())

#calculating the median of the existing patient's heart_rate data
median_heartrate = df_clinic['Heart_Rate'].median()
print(f"\nCalculated median heart rate to use for filling: {median_heartrate} BPM")

#filling blanks with median value
df_clinic['Heart_Rate_cleaned'] = df_clinic['Heart_Rate'].fillna(median_heartrate)

print("\n--- Step#3: Cleaned Clinical Data---")
print(df_clinic) ``
# System prompt
```You are a Clinical Data Integrity AI. Your task is to evaluate a newly cleaned patient record
and draft a professional warning note for the attending physician.

[CLEANED RECORD]
- Patient_ID: 902
- Age: 62
- Heart_Rate: 72.0 (Note: This value was missing in the raw log and was filled via Median Imputation).

INSTRUCTIONS FOR STEP-BY-STEP REASONING:
1. First, evaluate if a heart rate of 72.0 BPM is clinically normal or abnormal for a resting 62-year-old.
2. Second, consider the risk of relying on a data-imputed (statistically guessed) value during an active clinical diagnosis.
3. Third, generate a concise, 2-sentence warning flag for the electronic health record (EHR).

Output your step-by-step reasoning clearly, followed by the final warning flag.``
# AI's response
``Final EHR Warning Flag

Patient ID 902 has a recorded heart rate of 72.0 BPM, which falls within the normal resting range;
however, this value was generated through median imputation and was not directly measured.
Please obtain and verify an actual heart rate before using this value for clinical decision-making or treatment planning. ``
