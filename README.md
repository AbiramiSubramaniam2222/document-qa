🛠️ Badges 

![Python Version](https://img.shields.io/badge/Python-3.9%2B-blue)
![LangChain](https://img.shields.io/badge/LangChain-RAG-orange)
![FAISS](https://img.shields.io/badge/FAISS-Vector%20Search-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)



#Document Question-Answering System
##Overview

This project implements an end-to-end document question-answering pipeline. It uses LangChain, vector embeddings, FAISS, and LLMs to answer questions based on the content of PDFs or other text documents.

##Features

Automatic PDF extraction and smart text chunking

FAISS-based vector embeddings for fast similarity search

Retrieval-Augmented Generation (RAG) for accurate answers

Simple script-based interface (run inside Visual Studio Code)

Modular structure, easy to extend and customize

##Installation
'''1. Clone the repository
git clone https://github.com/AbiramiSubramaniam2222/document-qa.git
cd document-qa

2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

3. Install dependencies
pip install -r requirements.txt

Configuration

Use a .env file to store environment variables like API keys, model names, and file paths.

The system uses a parameter called max_size_tokens, which controls how much text is passed to the LLM per query.

In this project, it's set to 1000 tokens to avoid hitting model context limits while still returning good answers.

You can adjust chunking settings, embedding model, and other configs in config.yaml or similar files.

Usage

Since this project is run directly inside Visual Studio Code:

Run the script from VS Code’s terminal:

python3 document_qa_demo.py

Steps

Load a PDF from your local system (your script reads the file directly).

Ask a question in the terminal or script input.

The system retrieves relevant chunks using FAISS.

The LLM generates the final answer based on retrieved context.

Limitations

max_size_tokens = 1000 limits how much context the LLM can see at once.

Chunking strategy affects answer accuracy for large or dense PDFs.

Scanned PDFs require OCR before use.

Retrieval accuracy depends on embedding quality.

## Folder Structure

```
document-qa/
├── app.py                # Main application entry point (optional)
├── document_qa_demo.py   # Demo script you run inside VS Code
├── data/                 # Raw documents (you load PDFs from your local system)
├── embeddings/           # FAISS vector index files
├── requirements.txt      # Python dependencies
├── README.md             # Project documentation
├── venv/                 # Virtual environment (excluded from Git)
└── .gitignore            # Git ignore rules
```
```
📌 Architecture Overview
                  ┌────────────────────┐
                  │      PDF File      │
                  └─────────┬──────────┘
                            │ Extract text
                            ▼
                  ┌────────────────────┐
                  │   Text Chunking    │
                  │ (chunk + overlap)  │
                  └─────────┬──────────┘
                            │ Embed chunks
                            ▼
                  ┌────────────────────┐
                  │   Embedding Model  │
                  └─────────┬──────────┘
                            │ Store vectors
                            ▼
                  ┌────────────────────┐
                  │     FAISS Index     │
                  └─────────┬──────────┘
                            │ Retrieve top-K
                            ▼
                  ┌────────────────────┐
                  │ Retrieved Context   │
                  └─────────┬──────────┘
                            │ Send to LLM
                            ▼
                  ┌────────────────────┐
                  │     LLM Answer     │
                  └────────────────────┘
```
                  
```                
🔁 RAG Workflow Diagram (Simple & Clear)

User Question
      │
      ▼
Semantic Search (FAISS)
      │
      ▼
Retrieve Relevant Chunks
      │
      ▼
LLM + Retrieved Context
      │
      ▼
Final Grounded Answer
```

##📝 Example Input / Output
Input

PDF: Insurance Claim Policy Document
User Question:
“Is accidental damage covered under this policy?”

Output
Yes, accidental damage is covered. According to Section 2.1 of the policy,
the plan includes coverage for accidental physical damage to the insured item,
as long as the claim is filed within 30 days of the incident.
