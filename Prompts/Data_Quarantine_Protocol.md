# Project 'Calculated Z-Score mathematics'
# Goal 'Overcome the outlires in dataset and debugging mathematical traps'
# Python Script
import pandas as pd
import numpy as np

ward_data = {
    'Patient_ID': [1001, 1002, 1003, 1004, 1005, 1006, 1007],
    'Cholesterol': [180, 195, 210, 185, 950, 205, 190] 
}

df_ward = pd.DataFrame(ward_data)

#calculating the mean and standard devation
mean_chol = df_ward['Cholesterol'].mean()
std_chol = df_ward['Cholesterol'].std()

#calculating z-score of every patient
df_ward['Z_Score'] = (df_ward['Cholesterol'] - mean_chol) / std_chol
print("--- step#1: full ward analysis")
print(df_ward.round({'Z_Score': 2}))

outliers = df_ward[(df_ward['Z_Score'] > 2) | (df_ward['Z_Score'] < -2)]

print("\n--- Step#2: Critical outliers detected ---")
print(outliers.round({'Z_Score': 2}))
# Output
--- step#1: full ward analysis
   Patient_ID  Cholesterol  Z_Score
0        1001          180    -0.43
1        1002          195    -0.37
2        1003          210    -0.32
3        1004          185    -0.41
4        1005          950     2.27
5        1006          205    -0.34
6        1007          190    -0.39

--- Step#2: Critical outliers detected ---
   Patient_ID  Cholesterol  Z_Score
4        1005          950     2.27
# AI's generated Action Required
[DATA INTEGRITY ALERT: QUARANTINE ACTIVATED]
SECTION 2: The Action Required
The database administrator should immediately verify the source record to determine whether the value resulted from
a data-entry or transcription error (for example, an intended value such as 195 mg/dL or 250 mg/dL).
If the value is confirmed to be accurate, promptly notify the responsible clinical team so the patient's 
condition can be urgently assessed and appropriate escalation, including consideration of intensive monitoring or ICU evaluation if clinically indicated,
can be determined.
