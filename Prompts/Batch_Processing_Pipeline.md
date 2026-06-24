# Project: converting json files into DataFrame
# Goal: How to convert and add json file into dataSeet
# system prompt:
```You are an automated Clinical Data Pipeline Batch Processor. 
Your objective is to process a batch of unstructured medical texts and
output a valid JSON array containing structured patient records.

CRITICAL RULES:
1. If a specific data field (like Age or Billing_USD) is missing from the text, set its value to null. Do not guess.
2. Output ONLY the raw JSON array. No conversational text or introductions.

[BATCH INPUT DATA]

---
NOTE 1: "Patient Alice (ID: 501) is a 34yo female admitted for a routine elective appendectomy.
Total billing statements settled at 3200 USD."
---
NOTE 2: "Brought in an elderly male patient, ID 502, presenting with acute diabetic ketoacidosis.
Patient was unable to recall his exact age, but charts indicate an emergency admission. Total pharmacy bill is 1450 USD."
---
NOTE 3: "ID 503 is a 28-year-old female presenting with mild influenza symptoms. Admitted under urgent care status."
---

Expected JSON keys to extract for each entry:
- Patient_ID
- Age
- Gender
- Admission_Type
- Billing_USD.```
#AI repsonse:
```[{"Patient_ID":501,"Age":34,"Gender":"Female","Admission_Type":"Routine Elective","Billing_USD":3200},
{"Patient_ID":502,"Age":null,"Gender":"Male","Admission_Type":"Emergency","Billing_USD":1450},
{"Patient_ID":503,"Age":28,"Gender":"Female","Admission_Type":"Urgent Care","Billing_USD":null}]```

# Python Script
import pandas as pd
import json

ai_batch_output = [{"Patient_ID":501,"Age":34,"Gender":"Female","Admission_Type":"Routine Elective","Billing_USD":3200},
 {"Patient_ID":502,"Age":None,"Gender":"Male","Admission_Type":"Emergency","Billing_USD":1450},
  {"Patient_ID":503,"Age":28,"Gender":"Female","Admission_Type":"Urgent Care","Billing_USD":None}]

#converting the AI response in data frame
batch_df = pd.DataFrame(ai_batch_output)

print("--- Ai Batch Output in Data Frame---")
print(batch_df)

#for quick analysis: checking the total revenue collected from this batch, ignoring missing values
total_revenue = batch_df['Billing_USD'].sum()
print(f"\nTotal Revenue Generated Collected from this batch: ${total_revenue} USD")
