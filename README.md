# CIS-2777-Project-1

Course: CIS 2777 - Large  Language Models & Prompt Engineering
Instructor: John P. Baugh
Institution: Oakland Community College

-------------------------------
1.TASK DESCRIPTION
-------------------------------

Selected Task: 
Extracting Structured Information from Text

Task Overview:
The goal of this tsask is to extract unstructured clinical
data from a medical encounter note and format it into a standardized
JSON object. The required fields for the extraction are:
- Patient Information (Age, Gender)
- Cheif Complaint
- Primary Diagnosis
- Medications Prescribed (Name, Dosage, Frequency)
- Follow-up Timeline

Input Text:
"Patient is a 58-year-old female who presented to the clinic today complaining of 
persistent lower back pain for the past 3 weeks, radiating down her left leg. Pain 
is rated 7/10. After physical examination and review of lumbar spine imagining, the 
patient was diagnosed with Lumbar Radiculopathy (L5-S1). She was prescribed Naproxen 500 mg to be taken twice daily with food for inflammation, and Cyclobenzaprine 10 mg at bedtime as needed for muscle spasms. Patient was advised to attend physical therapy twice weekly and follow up with the clinic in 4 weeks."

------------------------------
2. PROMPT DESIGNS
------------------------------

--- Zero-Shot Prompt ---
Extract the structured information from the following medical note into JSON object. Include patient info, chief complaint, diagnosis, medications, and follow-up.

Input Text:
"Patient is a 58-year-old female who presented to the clinic today complaining of 
persistent lower back pain for the past 3 weeks, radiating down her left leg. Pain 
is rated 7/10. After physical examination and review of lumbar spine imagining, the 
patient was diagnosed with Lumbar Radiculopathy (L5-S1). She was prescribed Naproxen 500 mg to be taken twice daily with food for inflammation, and Cyclobenzaprine 10 mg at bedtime as needed for muscle spasms. Patient was advised to attend physical therapy twice weekly and follow up with the clinic in 4 weeks."

--- Few-Shot Prompt ---
You are a medical data extraction assistant. Extract structured information from medical notes into a strict JSON format with the keys."patient", "cheif_complaint", "diagnosis", "medications" (array of objects with "name", "dosage", "frequency"), and "follow_up".

### Example 1:
Input: 42-year-old male with acute right knee swelling after fall. Diagnosed with Right Knee Sprain. Prescribed Ibuprofen 800mg 3 times daily as needed. Return to clinic in 2 weeks.
Output:
{
    "patient": {"age": 42, "gender": "male"}
    "chief complaint": "acute right knee swelling after a fall",
    "diagnosis": "Right Knee Sprain",
    "medications": [
    {
    "name": "ibuprofen"
    "dosage": "800 mg",
    "frequency": "3 times daily as needed"
    }
    ],
    "follow_up": "2 weeks"
}

### Example 2:
Input: 65-year-old female presenting with shortness of breath and cough. Diagnosed with Community-Aquired Pneumonia. Prescribed Azithromycin 250mg once daily for 5 days. Re-evaluate in 10 days.
Output:
{
    "patient": {"age"; 65, "gender": "female"},
    "chief_complaint": "shortness of beath and cough",
    "diagnosis": "Community-Acquired Pneumonia",
    "medications": [
    {
    "name": "Azithromycin",
    "dosage": "250mg"
    "frequency": "once daily for 5 days"
    }
    ],
    "follow_up": "10 days"
}

### Input Text:
"Patient is a 58-year-old female who presented to the clinic today complaining of 
persistent lower back pain for the past 3 weeks, radiating down her left leg. Pain 
is rated 7/10. After physical examination and review of lumbar spine imagining, the 
patient was diagnosed with Lumbar Radiculopathy (L5-S1). She was prescribed Naproxen 500 mg to be taken twice daily with food for inflammation, and Cyclobenzaprine 10 mg at bedtime as needed for muscle spasms. Patient was advised to attend physical therapy twice weekly and follow up with the clinic in 4 weeks."

--- Many-Shot Prompt ---
You are a medical data extraction assistant. Extract structured information from medical notes into a strict JSON format with the keys: "patient", "chief_complaint", "diagnosis", "medications" (array of objects with "name", "dosage", "frequency") and "follow_up".

### Example 1:
Input: 42-year-old male with acute right knee swelling after fall. Diagnosed with Right Knee Sprain. Prescribed Ibuprofen 800mg 3 times daily as needed. Return to clinic in 2 weeks.
Output:
{"patient": {"age": 42, "gender": "male"}
"chief_complaint": "acute right knee swelling",
"diagnosis": "Right Knee Sprain",
"medications":
[{"name": "ibuprofen", "dosage": "800mg", "frequency": "3 times daily as needed"}]
"follow_up": "2 weeks"}

### Example 2:
Input: 65-year-old female presenting with shortness of breath and cough. Diagnosed with Community-Aquired Pneumonia. Prescribed Azithromycin 250mg once daily for 5 days. Re-evaluate in 10 days.
Output:
{"patient": {"age": 65, "gender": "female"},
"Cheif_complaint": "shortness of breath and cough",
"diagnosis": "Community-Acquired Pneumonia",
"medications":
[{"name": "Azithromycin", "dosage": "250mg", "frequency": "once daily for 5 days"}]
"follow_up": "10 days"}

### Example 3:
Input: 30-year-old female complaining of severe migraine with aura. Diagnosed with Migraine without aura rule out complex. Prescribed Sumatriptan 50mg as needed at onset. Follow up in 1 month.
Output:
{"patient": {"age: 30, "gender": "female"},
"chief_complaint": "severe migraine with aura",
"diagnosis": "Migraine",
"medications":
[{"name": "Sumatriptan", "dosage": "50mg", "frrequency": "as needed at onset"}],
"follow_up": "1 month"}

### Example 4:
Input: 50-year-old male presenting for routine hypertension checkup. Diagnosed with Essential Hypertension. Prescribed Lisinopril 10mg daily and Amlodipine 5mg dailu. Follow up in 3 months.
Output:
{"patient": {"age": 50, "gender": "male"},
"chief_complaint": "routine hypertension checkup",
"diagnosis": "Essential Hypertension",
"medications":
[{"name": "Lisinopril", "dosage": "10mg", "frequency": "daily"}, 
{"name": "Amlodipine", "dosage": "5mg", "frequency": "daily"}],
"follow_up": "3months}

### Example 5:
Input: 22-year-old male with persistent eczema flare-up on bilateral arms. Diagnoses with Atopic Dermatitis. Prescribed Hydrocortisone 2.5% cream aplly twice daily. Follow up in 6 weeks.
Output:
{"patient": {"age": 22, "gender": "male"},
"chief_complaint": "persistent eczema flare-up on bilateral arms", 
"diagnosis": :Atopic Dermatitis",
"medications"
[{"name": "Hydrocortozone 2.5% cream", "dosage": "apply thin layer", "frequency": "twice daily"}],
"follow_up": "6 weeks"}

#### Input Text:
"Patient is a 58-year-old female who presented to the clinic today complaining of 
persistent lower back pain for the past 3 weeks, radiating down her left leg. Pain 
is rated 7/10. After physical examination and review of lumbar spine imagining, the 
patient was diagnosed with Lumbar Radiculopathy (L5-S1). She was prescribed Naproxen 500 mg to be taken twice daily with food for inflammation, and Cyclobenzaprine 10 mg at bedtime as needed for muscle spasms. Patient was advised to attend physical therapy twice weekly and follow up with the clinic in 4 weeks."

-----------------------------
3. MODEL OUTPUTS
-----------------------------

--- Zero-Shot Output ---
{
    "patient_info": {
        "age": 58,
        "gender": "female"
    },
    "chief_complaint": "persistent lower back pain for the past 3 weeks, radiating down her left leg (Pain rated 7/10)",
    "diagnosis": "Lumbar Radiculopathy (L5-S1)",
    "medications": [
    {
    "drug": "Naproxen", 
    "dose": "500mg",
    "instructions": "twice daily with food for inflammation"
    },
    {
    "drug": "Cyclobenzaprine",
    "dose": "10mg",
    "instructions", "at bedtime as needed for muscle spasms"
    }
    ],
    "follow_up": "4 weeks (with clinic) and physical therapy twice weekly"
}

--- Few-Shot Output ---
{
    "patient": {
    "age": 58,
    "gender": "female"
    },
    "cheif_complaint": "persistent lower back pain radiating down left leg",
    "diagnosis": "Lumbar Radiculopathy (L5-S1)",
    "medications": [
    {
    "name": "Naproxen",
    "dosage": "500mg",
    "frequency": "twice daily with food"
    },
    {
    "name": "Cyclobenzaprine",
    "dosage": "10mg",
    "frequency": "at bedtime as needed"
    }
    ],
    "follow_up": "4 weeks"
}

--- Many-Shot Output ---
{"patient": {"age": 58, "gender": "female"},
"chief_complaint": "persistent lower back pain radiating down left leg", "diagnosis": "Lumbar Radiculopathy (L5-S1)", "medicatios":
[{"name": "Naproxen", "dosage": "500mg", "frequency": "twice daily with food"},{"name": "Cyclobenzaprine", "dosage": "10mg", "frequency": "at bedtime as needed"}],
"follow_up": "4weeks"}

-------------------------------
4.COMPARATIVE ANALYSIS
------------------------------

Schema Uniformity and keys:
-Zero-shot: While the output contained valid JSON and correctly identified all key facts, the model had to invent its own key schema (e.g., "patient_info", "drug", "dose", "instructions").
-Few-shot & Many-shot: Both prompts anchored the output schema perfectly to match the exact JSON keys supplied in the demonstration examples ("patient": "medications", "name", "dosage", "frequency").

Tokenization Effects and Output Formatting:
-Tolenizers process text by breaking down strings into common sub-word tokens. In JSON formatting, synta characters like dounle qoutes ("), colons (:), curly braces ({}), and newlines carry specific token patterns.
-In the Few-Shot prompt, multi-line formatted JSON examples conditioned the model's autoregressive indentations and newline tokens (\n).
-In the Many-Shot prompt, compact single-line JSON examples were deliberately used. The model mirrored this token pattern stricktly, emitting zero indentation or newline tokens, producing a fully minifield JSON string.

Context Window, Attention Focus, and Recency:
- Attention Mechanism: Large language models utilize self-attention mechanisms to weigh the relationships between tokens across the context window.
- Zero-Shot: The model relies heavily on its pre-trained parametric memory to decide how to structure the output.
- Few-Shot: Placing 2 examples directly before the target input created strong local attention heads pointing toward the structural template.
- Many-Shot: adding 5 examples loaded the prompt context with high example density. This amplified the model's pattern matching (in-context learning), ensuring that even minor semantic details were handled cleanly. Because the input prompt length remained well within context window limits (under 1,000 tokens), no perfprmance degradation or context decay occured.

-------------------------
5. REFLECTIONS
-------------------------

What Worked Best:
- Few-Shot Prompting struck the ideal balance between output precision, human readability, and token efficiency. It succesfully standardized the JSON keys while keeping the prompt concise.
- In-Context Learning (ICL): Demostrating the desired output format via examples proved vastly superior to writing abstract instructions alone.

What Failed or Degraded:
-Zero-Shot Key Variation: Without explicit structural examples, the zero-shot prompt produced extra conversational bloat in filed values and non-standard key names that would fail automated database parsing.
-Verbosity vs. Token Overhead in Many-Shot: While the many-shot prompt yielded rigid adherence to the target minified format, providing 5 examples added unnecessary prompt tokens without delivering meaningfull accuracy gains over the 2-shot version for a task of this complexity.

Future Improvements:
- Explicit Schema Constraints: Combine zero-shot/few-shot prompts with explicit JSON schema validation constraints or system-level instructions to enforce field constraints programmatically.
- Edge Case Examples in Few-Shot: Future few-shot prompts should include edge cases, such as handling missing fields (e.g., no follow-up listed or no prescribed medications) to teach the model hot to output null or empty arrays [].


