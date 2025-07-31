# Anemia Detection & Women's Health Assistant using GROQ + LangChain

## Link to project : https://colab.research.google.com/drive/1QTg5gglSh8dSLJ1z7tl0xcflT1_UpPt7?usp=sharing


This project is a Colab-based AI assistant that can:
-  Extract lab values from PDFs
-  Classify anemia types (Microcytic, Macrocytic, Normocytic)
-  Answer women's health questions using **GROQ's LLaMA3 model**
-  Use a custom knowledge base via **LangChain + FAISS + HuggingFace**

##  Features

-  Upload PDF or enter lab values manually
-  Automatic anemia classification based on Hemoglobin & MCV
-  Context-aware health Q&A using medical text from 'anemia.txt'
-  Answers generated using **LLM API (GROQ)** with contextual grounding
-  Optional support for Indian languages (via 'googletrans')

##  System Workflow

graph TD
A[User Input: PDF or Manual Values] --> B[Extract using pdfplumber]
B --> C[Anemia Classification]
C --> D[Show Lab Table & Diagnosis]
D --> E[Retrieve Relevant Info from anemia.txt]
E --> F[Send Query + Context to GROQ LLaMA3]
F --> G[Display Doctor's Answer]

##  Installation

Run the following in Google Colab:

!pip install pdfplumber ipywidgets googletrans==4.0.0-rc1 langchain faiss-cpu
!pip install -U sentence-transformers

Enable widget support in Colab:

from google.colab import output
output.enable_custom_widget_manager()

##  Model Details

| Component        | Technology / Model                               |
| ---------------- | ------------------------------------------------ |
| PDF Reading      | 'pdfplumber'                                     |
| Vector Search    | 'FAISS'                                          |
| Embeddings       | 'all-MiniLM-L6-v2' (via 'sentence-transformers') |
| LLM              | 'llama3-70b-8192' (via GROQ API)                 |
| Language Support | 'googletrans' (for multilingual UI/text)         |

## File Overview

Aaroogya_AI.ipynb → Main executable notebook
anemia.txt → Knowledge base file used for Q&A retrieval
README.md → This documentation

##  Normal Ranges for Anemia Detection

| Test       | Normal Range | Unit |
| ---------- | ------------ | ---- |
| Hemoglobin | 12.0 – 16.0  | g/dL |
| MCH        | 27.0 – 32.0  | pg   |
| MCHC       | 32.0 – 36.0  | g/dL |
| MCV        | 80.0 – 100.0 | fL   |

##  Anemia Diagnosis Logic

If Hemoglobin < 12.0:
  - If MCV < 80 → Microcytic Anemia
  - If MCV > 100 → Macrocytic Anemia
  - Else → Normocytic Anemia
Else:
  - Normal

## Example Output

Lab Report:
+-------------+-------------------+---------------+
| Name        | Normal Range      | Actual Value  |
+-------------+-------------------+---------------+
| Hemoglobin  | 12.0-16.0 g/dL    | 10.2          |
| MCH         | 27.0-32.0 pg      | 25.1          |
| MCHC        | 32.0-36.0 g/dL    | 30.9          |
| MCV         | 80.0-100.0 fL     | 71.5          |
+-------------+-------------------+---------------+

Diagnosis: Microcytic Anemia

Doctor's Answer:
This patient is likely experiencing iron deficiency anemia. Please follow up with iron panel tests.

##  API Key Configuration

GROQ_API_KEY = "api key"


