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

## Q1. Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?

### Answer

11 Tier-3 suppliers:

- Dravex Components India
- Plataforma Metales SA
- Maghreb Castworks
- Helios Pack Greece
- Cerromax Mineria
- Orinoco Pack SAPI
- Quetzal Textiles
- Sibertek Molding
- Archipelago PCB Corp
- Varna Electronics EAD
- Deltaforge Vietnam

All are High Risk with an active flag → Level 3 Activate per Policy §9 (CPO escalation + alternate supplier at minimum 40% volume).

---

## Q2. Which suppliers qualify for the annual Volume Rebate Program and how many are there?

### Answer

19 suppliers qualify:

- Borealis Composites
- Crestline Chemical Supply
- Fenwick Alloy Solutions
- Hanguk Circuit Works
- Hokkaido Alloy Tech
- Krauss-Polymex GmbH
- Lakeshore Components
- Lumivex Semiconductor NL
- Maplewood Polymer Corp
- Norbec Alloy Works
- Nordloom Finland Oy
- Orrentek Precision Mfg
- Ostwind Composites AG
- PrecisionForge Taiyuan
- Solveig Eco Packaging
- Straits Packaging Hub
- Tasman Circuit Boards
- Toreval Electronics
- Valdoro Special Alloys

Criteria (Policy §4.2):

- Tier-1
- OTD ≥ 93%
- Defect < 0.5%
- Sustainability Score ≥ 85

---

## Q3. Which region has the highest total PO value, and does it breach the concentration limit?

### Answer

EMEA at $193,987,179.91 — approximately 48.5% of total spend ($399,563,494.10).

This breaches the 45% regional concentration cap (Policy §5.3), requiring a Diversification Plan within 60 days.

---

## Q4. Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?

### Answer

11 suppliers (Compliance Score < 60):

- Deltaforge Vietnam
- Maghreb Castworks
- Helios Pack Greece
- Cerromax Mineria
- Orinoco Pack SAPI
- Varna Electronics EAD
- Quetzal Textiles
- Plataforma Metales SA
- Archipelago PCB Corp
- Dravex Components India
- Sibertek Molding

SWL restricts new PO issuance to 20% of prior quarter volume (Policy §3.4).

---

## Q5. Which product category has the highest average defect rate and does it exceed the Tier-2 limit?

### Answer

Mechanical Components — average 2.12% across 360 POs.

Below the Tier-2 ceiling of 2.50% (Policy §3.2), so no breach — but approaching the limit.

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
