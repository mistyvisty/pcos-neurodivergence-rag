# 🧠 PCOS × Neurodivergence — Medical RAG Assistant

> A Retrieval-Augmented Generation (RAG) pipeline grounded in real clinical research papers.  
> Answers questions about the PCOS–neurodivergence connection with cited evidence.

---

## 📌 What This Does

This notebook builds a **medical question-answering system** that:
- Ingests 5 peer-reviewed research papers on PCOS and neurodivergence
- Lets you ask natural language questions
- Returns answers **cited directly from the papers** (no hallucination)
- Refuses to answer if the papers don't contain relevant information

---

## 🗂️ Research Papers Used

> ⚠️ **PDFs are not included in this repo** — they are copyrighted academic papers.  
> Download them yourself using the links below and place them in the `papers/` folder.

| Filename | Paper | Access |
|----------|-------|--------|
| `pmos.pdf` | Cherskov et al. (2018) — *PCOS and Autism: A test of the prenatal sex steroid theory.* Translational Psychiatry. DOI: [10.1038/s41398-018-0186-7](https://doi.org/10.1038/s41398-018-0186-7) | 🔓 Open Access |
| `pmos1.pdf` | Redkar & Khan (2025) — *The impact of PCOS on attention: an empirical investigation.* BioPsychoSocial Medicine. DOI: [10.1186/s13030-024-00320-w](https://doi.org/10.1186/s13030-024-00320-w) | 🔓 Open Access |
| `pmos2.pdf` | Berni et al. (2018) — *PCOS is associated with adverse mental health and neurodevelopmental outcomes.* J Clin Endocrinol Metab. DOI: [10.1210/jc.2017-02667](https://doi.org/10.1210/jc.2017-02667) | 🔒 Paywall |
| `pmos3.pdf` | Dubey et al. (2021) — *Systematic review and meta-analysis: maternal PCOS and neuropsychiatric disorders in children.* Translational Psychiatry. DOI: [10.1038/s41398-021-01699-8](https://doi.org/10.1038/s41398-021-01699-8) | 🔓 Open Access |
| `pmos4.pdf` | Chen et al. (2020) — *PCOS or anovulatory infertility and offspring psychiatric disorders: a Finnish population-based cohort study.* Human Reproduction. DOI: [10.1093/humrep/deaa192](https://doi.org/10.1093/humrep/deaa192) | 🔓 Open Access |

> 💡 **Tip:** Papers marked 🔓 Open Access are freely downloadable from the DOI link directly.  
> For 🔒 paywalled papers, try [Unpaywall](https://unpaywall.org) or access via your institution.

---

## 🛠️ Tech Stack

| Component | Tool |
|-----------|------|
| PDF Extraction | PyMuPDF (fitz) |
| Chunking | LangChain RecursiveCharacterTextSplitter |
| Embeddings | HuggingFace `all-MiniLM-L6-v2` |
| Vector Store | FAISS |
| LLM | Groq — LLaMA 3.3 70B Versatile |
| Hallucination Guard | Custom system prompt refusing out-of-context answers |
| Citations | Author name + page number on every answer |
| Interactive UI | ipywidgets (no blocking input loop) |

---

## 🚀 How to Run

### 1. Open in Google Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

Upload `PCOS_Neurodivergence_RAG_v2.ipynb` to Google Colab.

### 2. Get a Free Groq API Key
- Go to [console.groq.com](https://console.groq.com)
- Create a free API key (starts with `gsk_`)
- In Colab: click the 🔑 key icon → **Add secret** → Name: `GROQ_API_KEY` → paste key → toggle ON

### 3. Download the Papers
- Download the 5 PDFs using the DOI links in the table above
- Rename them exactly: `pmos.pdf`, `pmos1.pdf`, `pmos2.pdf`, `pmos3.pdf`, `pmos4.pdf`

### 4. Run All Cells in Order
```
Step 1  → Install dependencies
Step 2  → Load & verify API key
Step 3  → Upload PDFs
Step 4  → Extract text from PDFs
Step 5  → Chunk documents
Step 6  → Build FAISS vector store
Step 7  → Set up Groq LLM + RAG chain
Step 8  → Query with sample questions
Step 9  → Inspect retrieved chunks (transparency)
Step 10 → Interactive Q&A widget
Bonus   → Paper coverage summary
```

---

## 💬 Example Questions & Answers

```python
ask("Are children of mothers with PCOS at higher risk of autism?")
# → Yes — studies found 35-60% increased odds [Cherskov 2018, Dubey 2021]

ask("How do elevated androgens in PCOS affect brain development?")
# → Via neuronal spine, synaptic plasticity, brain lateralization pathways

ask("What mental health disorders are most commonly associated with PCOS?")
# → Depression, anxiety, bipolar disorder, eating disorders [Berni 2018]

ask("Does insulin resistance in PCOS contribute to cognitive impairment?")
# → Yes — impairs glucose metabolism and neural processing [Redkar 2025]

ask("What is the prenatal sex steroid theory of autism?")
# → Elevated prenatal testosterone during neurological sex differentiation → autism risk

ask("What did the Finnish cohort study find about maternal PCOS?")
# → PCOS associated with 32% increased risk of ANY neuropsychiatric disorder in children
```

---

## 📋 Pipeline Overview

```
PDFs (research papers)
      ↓
Text Extraction (PyMuPDF)
      ↓
Chunking (RecursiveCharacterTextSplitter — 800 chars, 100 overlap)
      ↓
Embeddings (HuggingFace — all-MiniLM-L6-v2)
      ↓
Vector Store (FAISS — ~376 vectors)
      ↓
Query → Retrieve top-5 most relevant chunks
      ↓
LLM (Groq — LLaMA 3.3 70B) → Cited answer
```

---

## 📁 Repo Structure

```
pcos-neurodivergence-rag/
│
├── PCOS_Neurodivergence_RAG_v2.ipynb   ← main notebook
├── README.md                            ← this file
├── .gitignore                           ← excludes PDFs
└── papers/
    └── README.txt                       ← instructions to download papers
```

---

## ⚠️ Disclaimer

This tool is for **research and educational purposes only**.  
It is not a medical diagnostic tool. All answers are drawn directly from the uploaded research papers and should not be used as clinical advice. Always consult a qualified healthcare professional.

---

*Built by Preeti Bhardwaj | PCOS × Neurodivergence Research RAG*
