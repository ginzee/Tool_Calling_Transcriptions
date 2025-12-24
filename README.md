# Medical Transcript Structuring & ICD-10 Code Extraction (Synthetic Data)

**Author**  
Sam Ginzburg  
samginzee@gmail.com  

---

## Business Problem and Motivation

Medical professionals document patient encounters using free-text clinical notes that capture symptoms, diagnoses, procedures, and treatment plans. While these notes are rich in information, they are often written in inconsistent, dictation-style formats that make automated analysis difficult.

The goal of this project is to demonstrate how **large language models with tool calling (function calling)** can be used to:
- Extract structured medical fields from unstructured clinical transcriptions
- Standardize key information such as patient age and treatment plans
- Infer likely **ICD-10-CM diagnosis codes** from extracted treatments

This approach is directly applicable to healthcare operations such as medical documentation support, analytics, and insurance billing workflows.

---

## Data Source

The original project was inspired by a **guided learning exercise on DataCamp** using anonymized medical transcription data categorized by specialty.

To respect licensing and redistribution constraints, this repository **does not include the original dataset**. Instead, a **synthetic dataset** was generated to closely mirror:
- Column structure (`medical_specialty`, `transcription`)
- Data types and text length
- Dictation-style formatting
- Inconsistent headers, spacing, and section ordering
- Realistic clinical note “noise”

**Synthetic dataset used in this repository:**  
`data/synthetic_transcriptions_chaotic_v2.csv`

The synthetic transcriptions are newly generated and do not contain verbatim or near-duplicate content from the original dataset.

---

## Methods and Skills Demonstrated

This project demonstrates the following technical skills:

- **Natural Language Processing (NLP)**
  - Information extraction from unstructured clinical text
  - Schema-constrained outputs using tool calling
- **LLM Application Design**
  - OpenAI API usage
  - Function (tool) definition with JSON schema
  - Controlled model outputs via tool selection
- **Python & Data Engineering**
  - pandas
  - JSON parsing
  - Iterative API workflows
- **Responsible AI & Reproducibility**
  - Synthetic data generation for public sharing
  - Secure API key handling via environment variables
  - Clear, end-to-end notebook execution

---

## Methodology Overview

1. **Unstructured Input**
   - Each row contains a long, free-text medical transcription and an associated medical specialty.
   - Transcriptions include inconsistent formatting, dictation artifacts, and variable section headers.

2. **Structured Extraction via Tool Calling**
   - Custom tools are defined to extract:
     - Patient age
     - Medical specialty
     - Recommended treatment plan
   - Tool calling enforces schema compliance and reduces parsing errors.

3. **ICD-10-CM Code Inference**
   - The extracted treatment plan is passed to a separate tool that infers the most likely ICD-10-CM diagnosis code(s).
   - The model is constrained to return diagnosis codes only (no procedures or medications).

4. **Structured Output**
   - Results are stored in a pandas DataFrame (`df_structured`) suitable for downstream analytics or integration.

---

## Quick Glance at Results

Unstructured clinical text is transformed into clean, machine-readable fields:

- Patient age extracted from narrative text
- Specialty standardized from labels
- Treatment plans summarized from dense notes
- ICD-10-CM codes inferred for documentation and billing use cases

Example outputs are displayed directly in the notebook.

---

## How to Interpret the Results

- Tool calling enables reliable extraction even when transcription formatting is inconsistent.
- The approach scales across specialties without handcrafted rules.
- ICD-10-CM inference demonstrates how LLMs can assist—though not replace—medical coding workflows.

This pipeline is best viewed as a **decision-support prototype**, not a fully automated medical coding system.

---

## Environment Setup

To run this project locally:

1. Clone the repository
2. Install dependencies:
pip install pandas openai

csharp
Copy code
3. Create a `.env` file in the project root and add:
OPENAI_API_KEY=your_api_key_here

arduino
Copy code
4. Open and run:
tool_calling_raw.ipynb

yaml
Copy code

The `.env` file is excluded from version control.

---

## Credit

This project was inspired by a guided learning exercise on **DataCamp** and was extended with:
- Synthetic data generation
- Tool-calling–based extraction
- ICD-10-CM inference logic
- End-to-end reproducibility

All implementation, restructuring, and extensions are original.
