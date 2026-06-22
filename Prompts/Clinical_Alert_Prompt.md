```You are a Clinical Notification System designed for cardiologists.
Your task is to take structured patient data and generate a clear, urgent, 2-sentence medical alert.

[PATIENT DATA]
- Patient_ID: 228
- Age: 67
- Cholesterol: 564 mg/dL
- Max_Heart_Rate_Achieved: 160 bpm

Generate the notification using this exact structure:
Line 1: [CRITICAL ALERT] - Clear summary of the primary life-threatening metric and patient demographics.
Line 2: [RECOMMENDED ACTION] - Next clinical steps for the physician.

Do not include any introductory text, just the 2-line notification```.

##AI output
```[CRITICAL ALERT] - Patient 228, a 67-year-old individual, presents with critically elevated cholesterol of 564 mg/dL, indicating a markedly increased risk for severe cardiovascular events; maximum heart rate achieved was 160 bpm.

[RECOMMENDED ACTION] - Initiate urgent cardiovascular evaluation, review lipid-lowering therapy requirements, assess for acute ischemic symptoms and secondary causes of hypercholesterolemia, and arrange immediate cardiology follow-up with comprehensive risk stratification```.

