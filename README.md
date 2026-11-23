# NCERT Class 11 & 12 Physics AI Tutor (End-to-End RAG Pipeline)

![Databricks](https://shields.io)
![MLflow](https://shields.io)
![Vector Search](https://shields.io)
![License](https://shields.io)

## 💬 Live Web Application

**Launch NCERT Physics Tutor App** (`ncert-physics-tutor` on Databricks Apps)

Ask conceptual physics questions, derivations, and numerical problems grounded directly in official NCERT Class 11 & 12 Physics textbooks.

## 🎯 Project Overview

End-to-end **Retrieval-Augmented Generation (RAG) and automated document ingestion pipeline** built on Databricks using Unity Catalog, `ai_parse_document`, Mosaic AI Vector Search, MLflow `ResponsesAgent`, and Databricks Apps.

## 🏗 Architecture

```text
┌────────────────────────────────────────────────────────┐
│ 1. DATA & VECTOR PIPELINE (Event-Driven)               │
├────────────────────────────────────────────────────────┤
│ UC Volume PDFs → ai_parse_document → Delta Sync Index  │
│ (File Arrival)   (1,500-char chunks) (Managed Embed)   │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 2. AGENT & SERVING PIPELINE (Mosaic AI + MLflow)       │
├────────────────────────────────────────────────────────┤
│ Top-6 Retriever → Qwen 3.5 (122B)   → Model Serving    │
│ (Vector Search)   (5-Step + Unicode)  (Scale-to-zero)  │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 3. FRONTEND LAYER (Databricks Apps)                    │
├────────────────────────────────────────────────────────┤
│ Student Query   → ncert-physics-tutor → Clean Unicode  │
│ (Physics Q&A)     (Web Chat UI)         & NCERT Ref    │
└────────────────────────────────────────────────────────┘
```


## 🛠 Technologies

| Component | Technology |
| :--- | :--- |
| **Platform** | Databricks (Unity Catalog, Serverless Compute) |
| **Document Parsing** | Databricks `ai_parse_document` (v2.0 with figure descriptions) |
| **Data Processing** | PySpark, Delta Lake (Change Data Feed enabled) |
| **Vector Database** | Mosaic AI Vector Search (Delta Sync + Managed Embeddings) |
| **LLM & Agent Framework** | `databricks-qwen35-122b-a10b`, MLflow `ResponsesAgent` |
| **Orchestration** | Databricks Jobs (File Arrival Trigger) |
| **Frontend UI** | Databricks Apps (`e2e-chatbot-app-next`) |

## 📁 Project Structure

*   `Parse_Document.ipynb`: Parses raw PDFs from Unity Catalog Volumes and writes to Delta Lake.
*   `sync_ncert_index.ipynb`: Runs incremental Delta Syncs for Vector Search.
*   `driver.ipynb`: Configures the `VectorSearchRetrieverTool`, system prompts, and deployment endpoints.
*   `Jobs/NCERT_Physics_Auto_Ingest`: Event-driven workflow triggered by file arrivals.
*   `App/ncert-physics-tutor`: React/Next.js web chat interface hosted on Databricks Apps.

## 🚀 Deployment & License

The pipeline uses Unity Catalog and serverless endpoints with scale-to-zero enabled. This project is licensed under the Apache-2.0 License.

## 🙋 Author & Acknowledgments

**Saantanu**  
📧 saantanu15@gmail.com | luckyboyshantanu@gmail.com  
🔗 [GitHub](https://github.com/saantanu15-sketch)

Built using Databricks and NCERT resources.

**⭐ Star this repo if you found it helpful!**
