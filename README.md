# SCM Assistant Bot

A Retrieval-Augmented Generation (RAG) chatbot built using Flowise for answering Supply Chain Management (SCM) questions using supplier performance datasets and governance policy documents.

---

# Public Chatbot URL

```txt
[Paste your deployed public URL here]
```

---

# Project Overview

This project was developed as part of an AI Engineer Case Study Assessment.

The chatbot answers supplier governance and procurement-related questions using:

- Supplier Performance CSV dataset
- Supply Chain Governance Policy PDF
- Flowise RAG Pipeline
- Groq LLM
- HuggingFace Embeddings
- Pinecone Vector Database

The chatbot retrieves relevant supplier records and governance rules, then combines them to generate context-aware responses.

---

# Technologies Used

| Component | Technology |
|---|---|
| Framework | Flowise |
| LLM | Groq - llama-3.3-70b-versatile |
| Embeddings | HuggingFace BAAI/bge-small-en-v1.5 |
| Vector Database | Pinecone |
| Retrieval | Document Store Retriever |
| Chain | Conversational Retrieval QA |
| Memory | Buffer Memory |
| Data Sources | CSV + PDF |

---

# Files Used

| File | Purpose |
|---|---|
| supplier_performance_data.csv | Supplier performance metrics |
| SupplyChain_Governance_Policy_v3.2.pdf | Governance rules and policies |
| scm_assistant.json | Exported Flowise chatflow |

---

# Flowise Setup Process

## Step 1: Create Flowise Workspace

- Login to Flowise
- Create a new Chatflow
- Create a Document Store

Created document store:

```txt
SCM_documents
```

---

## Step 2: Upload Data Sources

Uploaded:

- SupplyChain_Governance_Policy_v3.2.pdf
- supplier_performance_data.csv

Configured:

- Recursive Character Text Splitter
- HuggingFace Embeddings
- Pinecone Vector Store

---

# Chunk Configurations Tried

## Configuration A

| Setting | Value |
|---|---|
| Chunk Size | 1000 |
| Chunk Overlap | 200 |

### Results

| File | Chunks |
|---|---|
| PDF | 19 |
| CSV | 2000 |

---

## Configuration B

| Setting | Value |
|---|---|
| Chunk Size | 500 |
| Chunk Overlap | 100 |

### Results

| File | Chunks |
|---|---|
| PDF | 35 |
| CSV | 4000 |

---

# Embedding Configuration

| Setting | Value |
|---|---|
| Embedding Model | BAAI/bge-small-en-v1.5 |
| Provider | HuggingFace |
| Vector DB | Pinecone |
| Namespace | scm |

---

# LLM Configuration

| Setting | Value |
|---|---|
| Provider | Groq |
| Model | llama-3.3-70b-versatile |
| Temperature | 0.0 |
| Streaming | Enabled |

---

# Chatflow Architecture

The Flowise pipeline contains:

1. Groq Chat Model
2. Document Store Retriever
3. Conversational Retrieval QA Chain
4. Buffer Memory

Workflow:

```txt
User Query
     ↓
Retriever
     ↓
Relevant Chunks
     ↓
Groq LLM
     ↓
Policy Analysis
     ↓
Final Response
```

---

# Prompt Engineering

## System Prompt

```txt
You are SCM Assistant for BQBYTE Technologies.

Use only the retrieved supplier performance data and governance policy.

Rules:

1. Never invent supplier data.
2. Use policy rules while answering.
3. Mention supplier metrics whenever available:
   - OTD Rate
   - Compliance Score
   - Defect Rate
   - Risk Level
   - Sustainability Score

4. Mention policy sections when applicable.

5. If insufficient information exists say:
"The supplied documents do not contain enough information."

Response format:

Supplier:
[Supplier ID]

Metrics:
• OTD:
• Compliance:
• Defect:
• Sustainability:
• Risk:

Policy Analysis:
[Applicable rules]

Recommendation:
[Suggested action]
```

---

# Retrieval Improvements Applied

The following improvements were added for better RAG performance:

✓ Increased Top-K retrieval to 10

✓ Added Buffer Memory

✓ Enabled Source Document Retrieval

✓ Reduced temperature to 0.0

✓ Added custom SCM system prompt

✓ Used PDF + CSV combined retrieval

These changes reduced hallucinations and improved response accuracy.

---

# Sample Questions

## Q1

```txt
What happens if compliance score falls below 60?
```

Expected output:

- Supplier Watch List (SWL)
- New purchase orders limited to 20% of prior quarter volume

---

## Q2

```txt
Does SUP-005 qualify for Tier-1 rebate?
```

Expected reasoning:

- OTD ≥93%
- Defect <0.5%
- Sustainability ≥85

Then determine eligibility.

---

## Q3

```txt
Which suppliers have compliance below 60?
```

Expected output:

List supplier IDs and explain SWL implications.

---

## Q4

```txt
Which suppliers are near ELTRP boundaries?
```

Expected output:

- SUP-005
- SUP-012
- SUP-015
- SUP-023

---

## Q5

```txt
What certifications are required for electronic component suppliers?
```

Expected output:

- ISO 9001
- RoHS Compliance
- AEC-Q100 recommendation where applicable

---

# Repository Structure

```txt
scm-assistant/
│
├── README.md
├── scm_assistant.json
├── screenshots/
├── .gitignore
```

---

# Screenshots Included

Inside:

```txt
/screenshots
```

Contains:

- Flowise Dashboard
- Document Store Creation
- PDF Upload
- CSV Upload
- Pinecone Configuration
- Chatflow Canvas
- Final Architecture

---

# Future Improvements

If given additional development time:

- Hybrid Search (BM25 + Vector Search)
- Metadata Filtering
- Source Citation Display
- Advanced Reranking
- Dashboard Analytics
- Multi-agent Query Routing
- Better Memory Handling
- UI Improvements

---

# Submission Contents

Repository includes:

- README.md
- scm_assistant.json
- screenshots/
- .gitignore

---

# Author

Pallab Mandal  
B.Tech Student
