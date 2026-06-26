# Project: Cleaned messy data in python using 'Regex'
# Goal: to remove messy and unwanted objects in the dataset and converted their datatype as required
# Python script:
``import pandas as pd

messy_data = {
    'Patient_ID': [801, 802, 803, 804],
    'Symptom': ['Chest Pain', 'Arrhythmia', 'Influenza', 'Hypertension'],
    'Messy_Bill': ['$1,200 USD', ' $450 ', '$3,100.50 USD', '$980']
}

df_messy = pd.DataFrame(messy_data)

print("--- Messy Healthcare Data(before cleaning) ---")
print(df_messy)
print(df_messy.dtypes)

#cleaning data using regex
char_to_remove = r'[\$,\sUSD]'
df_messy['Clean_Bill'] = df_messy['Messy_Bill'].str.replace(char_to_remove, '', regex=True)

df_messy['Clean_Bill'] = df_messy['Clean_Bill'].astype(float)

print("\n--- Messy Healthcare Data(after cleaning) ---")
print(df_messy)
print(df_messy.dtypes)

avreage_bill = df_messy['Clean_Bill'].mean()
print(f"\nAverage Healthcare Bill: ${avreage_bill}")``

# System prompt:
``You are a Medical Billing Localization Assistant.
Your job is to take a clean, raw numeric dictionary and format it into a professional, human-readable billing summary.

[RAW DATA]
{
    "Patient_ID": 803,
    "Symptom": "Arrhythmia",
    "Clean_Bill": 3100.50
}

Format Requirements:
1. State the patient's ID and clinical presentation clearly.
2. Format the Clean_Bill into standard financial text notation: round it strictly to 2 decimal places and prefix it with a dollar sign (e.g., $X,XXX.XX).
3. Provide a standard insurance disclaimer sentence at the end.

Output ONLY the localized summary paragraph. No conversational introductions.``

# AI's response:
``Patient ID 803 presented with arrhythmia. The total clean bill is **$3,100.50**.
This amount is subject to insurance verification, coverage, and applicable policy terms.``
