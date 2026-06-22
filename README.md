# Research Paper RAG Assistant (V2.1)

A custom Retrieval-Augmented Generation (RAG) system designed to answer questions from academic research papers across both single-column and IEEE two-column formats.

This project was built from scratch to understand the complete RAG pipeline, including document parsing, chunking, semantic retrieval, vector search, and answer generation without relying on high-level RAG frameworks.

---

Current capabilities:

- PDF text extraction
- Metadata extraction
- Section detection
- Section-aware chunking
- Semantic embeddings
- FAISS retrieval
- Query routing
- Local LLM-based answer generation
- Support for multiple academic paper formats

---

## Project Motivation

Research papers are often long and difficult to navigate. Traditional keyword search struggles to retrieve semantically relevant information from complex academic documents.

This project explores how Retrieval-Augmented Generation (RAG) can be used to build an intelligent research assistant capable of:

- Understanding paper content
- Retrieving relevant information
- Answering natural language questions
- Summarizing methodologies and findings

---

## Architecture

```text
PDF
 │
 ▼
PyMuPDF Extraction
 │
 ▼
Metadata / Content Separation
 │
 ▼
Section Detection
 │
 ▼
Section-aware Chunking
 │
 ▼
Sentence Transformer Embeddings
 │
 ▼
FAISS Vector Store
 │
 ▼
Query Routing
 │
 ▼
Semantic Retrieval
 │
 ▼
Local LLM (Qwen via Ollama)
 │
 ▼
Answer Generation
```

---

## Technologies Used

### Document Processing

- PyMuPDF

### NLP & Embeddings

- Sentence Transformers
- all-MiniLM-L6-v2

### Vector Database

- FAISS

### LLM Inference

- Ollama
- Qwen 2.5

### Machine Learning Utilities

- NumPy
- Scikit-Learn

---

## Pipeline Overview

### 1. PDF Extraction

Research papers are parsed using PyMuPDF to extract raw text content.

### 2. Metadata Extraction

Content appearing before the abstract section is separated and stored as metadata.

Examples:

- Title
- Authors
- Affiliations
- Email addresses

### 3. Section Detection

The system identifies major sections such as:

- Abstract
- Introduction
- Methodology
- Results
- Conclusion

Section detection is used to improve retrieval precision.

### 4. Section-Aware Chunking

Each section is divided into overlapping chunks while preserving contextual continuity.

### 5. Embedding Generation

Chunks are converted into dense vector embeddings using Sentence Transformers.

### 6. Vector Storage

Embeddings are stored in a FAISS index for efficient similarity search.

### 7. Query Routing

User questions are mapped to the most relevant sections before retrieval.

Examples:

| Query | Routed Section |
|---------|---------|
| What is the objective of the paper? | Abstract, Introduction |
| Summarize the methodology | Methodology |
| What results were obtained? | Results |

### 8. Semantic Retrieval

The most relevant chunks are retrieved using cosine similarity search over the FAISS index.

### 9. Answer Generation

Retrieved context is passed to a local LLM which generates the final answer.

---

## Example Questions

The assistant can answer questions such as:

- What is the objective of the paper?
- Who are the authors?
- Which dataset was used?
- Summarize the proposed model.
- What evaluation metrics were used?
- What were the key findings?
- What limitations were discussed?

---

## Experimental Evaluation

The system was evaluated on:

- Single-column journal papers
- IEEE two-column conference papers
- Previously unseen research papers

### Observations

*Embeddings consistently captured semantic meaning.

*FAISS retrieval returned highly relevant chunks.

*Generation quality was generally accurate with limited hallucinations.

*Section-aware retrieval improved retrieval precision.

*The system remained functional even when section detection failed.

*Metadata extraction occasionally struggled on certain IEEE paper layouts.

*Local generation models introduced noticeable latency.

---

## Key Findings

One of the most interesting findings was that retrieval performance remained strong even when section detection failed.

This suggests that:

- Semantic embeddings are highly effective.
- FAISS retrieval provides strong robustness.
- Section detection improves performance but is not a hard dependency.

This behavior was observed during testing on previously unseen IEEE papers.

---

## Current Limitations

- Metadata extraction is not fully robust across all paper formats.
- Section detection may fail for unusual layouts.
- Local generation models can be slow on CPU-only environments.
- No frontend interface yet.

---

## Future Work

### Version 3

Planned improvements:

- Hybrid Retrieval (BM25 + Dense Retrieval)
- Better metadata extraction
- Faster local generation models
- Retrieval reranking
- Streamlit frontend
- Multi-paper support
- Citation-aware answering

---

## Repository Structure


Research-Paper-RAG-Assistant/
│
├── ResearchAssistant.ipynb
├── README.md
├── requirements.txt



---

## Learning Outcomes

This project was built as part of a hands-on exploration of Retrieval-Augmented Generation.

Concepts explored include:

- PDF Parsing
- Chunking Strategies
- Embedding Models
- Vector Databases
- Semantic Retrieval
- Query Routing
- Local LLM Inference
- RAG Evaluation



## Milestone

🚀 Research Assistant V2.1 – First RAG Milestone Completed
