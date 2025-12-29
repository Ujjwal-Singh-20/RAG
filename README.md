# RAG Chatbot with Qdrant + Streamlit

This project is a simple Retrieval-Augmented Generation (RAG) chatbot built with **Streamlit** and **Qdrant**.  
It allows users to upload PDFs, chunk and embed them, store embeddings in Qdrant, and query them interactively.

---

## Flow Overview

1. **Login to Qdrant cloud**
    - https://qdrant.tech/documentation/cloud-quickstart/
    - follow the instructions to setup a new cluster and use the credentials in `.env` file in the codebase

2. **Environment Setup**
   - Load environment variables (`QDRANT_CONSOLE_URL`, `QDRANT_API_KEY`) in the `.env`

3. **User Identity**
   - Each user gets a persistent **Device ID** (auto-generated and stored in local storage)
   - Optionally, users can set a **Custom ID** (8 characters)
   - Active ID is used to scope documents per user.

4. **PDF Upload**
   - Users upload one or more PDFs via Streamlit.
   - Each PDF is:
     - **Chunked** into smaller text segments (`chunk_pdf`).
     - **Embedded** into vectors (`embed_texts`).
     - **Upserted** into Qdrant with metadata (user_id, filename, page, chunk index).

5. **Document Management**
   - Uploaded PDFs are listed for the active user.
   - Users can delete documents using the ❌ in the streamlit UI, which removes them from Qdrant.

6. **Querying**
   - Users type a question in the input box.
   - The query is embedded (`embed_query`) and searched against Qdrant.
   - Results are displayed with:
     - Document name
     - Page/chunk info
     - Similarity score
     - Retrieved text from the uploaded documents

---

## 🛠️ Key Files

- `main.py` - Streamlit app entry point.
- `pipeline/chunk_pdf.py` - PDF chunking logic.
- `pipeline/embed_chunks.py` - Embedding functions.
- `qdrant_operations.py` - Qdrant helper functions (upsert, search, delete, list).

---

## ⚡ Quick Start

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
2. Set up `.env` with your Qdrant URL and API key.

3. Run the app:  
    ```bash
    streamlit run main.py
4. Upload PDFs, ask questions, and explore results




# Each user’s data is isolated by their active ID(user_id).
## Multi Tenancy -  https://qdrant.tech/documentation/guides/multitenancy/