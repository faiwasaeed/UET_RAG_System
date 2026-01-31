# 🎓 UET Prospectus RAG System

> An intelligent Retrieval-Augmented Generation (RAG) system for querying university prospectus information using natural language.

[![Python](https://img.shields.io/badge/Python-3.12%2B-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104%2B-009688.svg)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-FF4B4B.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Demo](#demo)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Configuration](#configuration)
- [API Documentation](#api-documentation)
- [Performance](#performance)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Acknowledgments](#acknowledgments)

## 🌟 Overview

The **UET Prospectus RAG System** is an AI-powered question-answering system designed to help students, parents, and administrators quickly find information from the University of Engineering and Technology (UET) Lahore prospectus. Instead of manually searching through hundreds of pages, users can simply ask questions in natural language and receive accurate, contextual answers.

### What is RAG?

**Retrieval-Augmented Generation (RAG)** is an AI framework that enhances large language model outputs by incorporating relevant information retrieved from external knowledge bases. This system combines:

- 🔍 **Semantic Search**: Find relevant information using meaning, not just keywords
- 🧠 **Local LLM**: Privacy-preserving answer generation using Gemma3
- 📚 **Vector Database**: Fast similarity search across document chunks
- 🎯 **Smart Reranking**: Intelligent relevance scoring for accurate results

## ✨ Features

### Core Capabilities

- ✅ **Natural Language Queries**: Ask questions like "Who is the chairperson of Computer Science?"
- ✅ **Multi-Query Expansion**: Automatically generates query variants for better recall
- ✅ **Intelligent Reranking**: Custom scoring algorithm prioritizes most relevant results
- ✅ **Source Attribution**: Every answer includes page numbers and department tags
- ✅ **Local Deployment**: Privacy-preserving with no external API calls
- ✅ **Fast Response**: Sub-5-second answers for most queries
- ✅ **Rich Metadata**: Department tagging and section classification

### Advanced Features

- 🔄 **MMR Retrieval**: Maximal Marginal Relevance for diverse results
- 🏷️ **Metadata Filtering**: Filter by department, section type, and page
- 📊 **Performance Monitoring**: Real-time query statistics and timing
- 🛡️ **Guardrails**: UET-specific relevance checking
- 🎨 **Modern UI**: Clean Streamlit interface with sample questions
- 📖 **API-First**: RESTful FastAPI backend for easy integration

## 🏗️ Architecture

[Architecture Diagram]<img width="5970" height="4170" alt="UET_RAG_Architecture_Infographic" src="https://github.com/user-attachments/assets/9284ba75-9a00-4548-80b3-26f5d5149c27" />


### System Layers

1. **Data Ingestion Layer**: PDF loading, text cleaning, chunking, and metadata extraction
2. **Vector Storage Layer**: ChromaDB with cosine similarity and HNSW indexing
3. **Query Processing Layer**: Validation, expansion, and embedding generation
4. **Retrieval & Ranking Layer**: Semantic search with MMR and custom reranking
5. **Generation Layer**: Context building and LLM-based answer generation
6. **Application Layer**: FastAPI backend and Streamlit frontend

### Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Embeddings** | nomic-embed-text (Ollama) | 768-dim vector generation |
| **Vector DB** | ChromaDB | Persistent vector storage |
| **LLM** | Gemma3 (Ollama) | Answer generation |
| **Framework** | LangChain | RAG pipeline orchestration |
| **API** | FastAPI | RESTful web service |
| **UI** | Streamlit | Interactive chat interface |
| **PDF Processing** | PyPDFLoader | Document extraction |
| **Language** | Python 3.12+ | Core implementation |

## 🎬 Demo

### Example Queries

```
Q: Who is the chairperson of the Department of Computer Science?
A: Dr. [Name] is the current chairperson of the Department of Computer Science.

Q: Which department offers the M.Sc. Artificial Intelligence program?
A: The M.Sc. in Artificial Intelligence program is offered by the Department of Computer Science.

Q: What are the admission requirements for Electrical Engineering?
A: Admission requirements include [specific details from prospectus]...
```

### Screenshots

**Chat Interface:**
```
┌─────────────────────────────────────┐
│  🎓 UET AI Assistant                │
├─────────────────────────────────────┤
│ 👤 You: Who is the dean of CS?     │
│                                     │
│ 🤖 UET Assistant (2.3s):            │
│ The Dean of the Faculty of...      │
└─────────────────────────────────────┘
```

## 🚀 Installation

### Prerequisites

- **Python**: 3.12 or higher
- **Ollama**: For local LLM inference
- **RAM**: 8GB minimum (16GB recommended)
- **Storage**: 10GB free space
- **OS**: Linux, macOS, or Windows (with WSL)

### Step 1: Install Ollama

```bash
# Linux/macOS
curl -fsSL https://ollama.ai/install.sh | sh

# Windows
# Download from https://ollama.ai/download
```

### Step 2: Pull Required Models

```bash
ollama pull nomic-embed-text
ollama pull gemma3
```

### Step 3: Clone Repository

```bash
git clone https://github.com/faiwasaeed/uet-rag-system.git
cd uet-rag-system
```

### Step 4: Create Virtual Environment

```bash
python -m venv venv

# Activate
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows
```

### Step 5: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 6: Add Your Prospectus

Place your UET prospectus PDF in the `data/` directory:

```bash
mkdir -p data
# Copy your PDF to: data/UET lahore Document.pdf
```

## 🎯 Quick Start

### 1. Ingest Data (First Time Only)

```bash
python ingest.py
```

This will:
- Load the PDF document
- Clean and chunk the text
- Generate embeddings
- Store in ChromaDB vector database

**Expected output:**
```
🚀 Starting Enhanced Data Ingestion...
📄 Loaded 250 pages.
✂️ Split into 5243 chunks.
🏷️ Adding metadata to chunks...
⏳ Generating Embeddings (this may take a moment)...
💾 Vector Database saved to data/vector_db
✅ Ingestion complete! Total chunks: 5243
```

### 2. Start the API Server

```bash
python main.py
```

**Output:**
```
🚀 Starting UET AI Agent API...
📚 Make sure you've run ingest.py first!
🌐 API will be available at: http://localhost:8000
📖 Documentation at: http://localhost:8000/docs
INFO:     Started server process
INFO:     Uvicorn running on http://0.0.0.0:8000
```

### 3. Launch the Web Interface

In a **new terminal** (keep the API running):

```bash
streamlit run app.py
```

**Output:**
```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
  Network URL: http://192.168.1.x:8501
```

### 4. Start Chatting!

Open http://localhost:8501 in your browser and start asking questions about UET!

## 💻 Usage

### Web Interface

1. **Open Browser**: Navigate to http://localhost:8501
2. **Ask Questions**: Type your query or click a sample question
3. **View Answers**: Get instant responses with source attribution
4. **Check Stats**: Monitor query count and response times in the sidebar

### API Usage

#### Using cURL

```bash
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"message": "Who is the chairperson of Computer Science?"}'
```

#### Using Python

```python
import requests

response = requests.post(
    "http://localhost:8000/chat",
    json={"message": "What programs does the CS department offer?"}
)

data = response.json()
print(f"Answer: {data['response']}")
print(f"Processing time: {data['processing_time']}s")
```

#### Response Format

```json
{
  "response": "The Department of Computer Science offers programs including...",
  "processing_time": 2.34,
  "status": "success"
}
```

### Command Line Testing

```bash
# Test the agent directly
python agent.py
```

This runs built-in test cases for validation.

## 📁 Project Structure

```
uet-rag-system/
│
├── data/                          # Data directory
│   ├── UET lahore Document.pdf    # Input PDF (user-provided)
│   └── vector_db/                 # ChromaDB storage (auto-generated)
│
├── ingest.py                      # Data ingestion script
├── agent.py                       # RAG agent logic
├── main.py                        # FastAPI backend
├── app.py                         # Streamlit frontend
│
├── requirements.txt               # Python dependencies
├── README.md                      # This file
├── LICENSE                        # License file
│
└── docs/                          # Documentation
    ├── architecture_infographic.png
    └── technical_report.pdf
```

### File Descriptions

| File | Purpose | Key Functions |
|------|---------|---------------|
| `ingest.py` | Data ingestion & indexing | `ingest_data()`, `clean_text()`, `extract_metadata()` |
| `agent.py` | RAG pipeline & retrieval | `process_query()`, `search_prospectus()`, `expand_query()` |
| `main.py` | API server | FastAPI endpoints: `/`, `/health`, `/chat` |
| `app.py` | Web UI | Streamlit chat interface with statistics |

## 🔧 How It Works

### 1. Offline Indexing (One-Time)

```
PDF Document
    ↓
Text Extraction → Cleaning → Chunking (800/300)
    ↓
Metadata Tagging (departments, sections)
    ↓
Embedding Generation (nomic-embed-text)
    ↓
Vector Storage (ChromaDB)
```

### 2. Online Query Processing (Per Query)

```
User Query
    ↓
Validation & Guardrails
    ↓
Query Expansion (4 variants)
    ↓
Embedding Generation
    ↓
Semantic Search (MMR, k=4, fetch_k=15)
    ↓
Deduplication
    ↓
Custom Reranking (phrase match, keywords, boosting)
    ↓
Top-6 Selection
    ↓
Context Construction
    ↓
LLM Generation (Gemma3, temp=0)
    ↓
Response Delivery
```

### 3. Key Algorithms

#### Query Expansion

Generates multiple query variants to improve recall:

```python
Original: "Who is the chairperson of Computer Science?"

Variants:
1. "Who is the chairperson of Computer Science?"
2. "faculty list Computer Science"
3. "staff members Computer Science"
4. "Computer Science department faculty"
```

#### Reranking Scores

Documents are scored based on:

- **Exact Phrase Match**: +40 per 4-word phrase
- **Keyword Match**: +2 per matching keyword
- **Faculty Terms**: +15 if query is about faculty
- **Department Match**: +10 if department name appears

Example:
```
Query: "chairperson of computer science"
Document: "Dr. John Smith is the Chairperson of Computer Science..."

Score Breakdown:
+ 40 (exact 4-word phrase: "chairperson of computer science")
+ 6  (3 keywords matched)
+ 15 (contains faculty term: "Chairperson")
+ 10 (department match: "Computer Science")
─────
= 71 (High relevance!)
```

## ⚙️ Configuration

### Chunking Parameters

```python
# in ingest.py
CHUNK_SIZE = 800        # Characters per chunk
CHUNK_OVERLAP = 300     # Overlap between chunks
```

### Retrieval Parameters

```python
# in agent.py
MMR_K = 4              # Documents per query variant
MMR_FETCH_K = 15       # Candidate pool size
MMR_LAMBDA = 0.5       # Relevance vs diversity (0-1)
TOP_K_DOCUMENTS = 6    # Final documents for context
```

### LLM Parameters

```python
# in agent.py
MODEL = "gemma3"
TEMPERATURE = 0        # Deterministic responses
```

### API Configuration

```python
# in main.py
HOST = "0.0.0.0"
PORT = 8000
TIMEOUT = 180          # seconds
```

## 📚 API Documentation

### Endpoints

#### GET `/`

Health check and service information.

**Response:**
```json
{
  "status": "online",
  "service": "UET AI Agent API",
  "version": "2.0",
  "endpoints": {
    "/chat": "POST - Send questions about UET",
    "/health": "GET - Check service health"
  }
}
```

#### GET `/health`

Detailed health status.

**Response:**
```json
{
  "status": "healthy",
  "timestamp": 1706745600.123
}
```

#### POST `/chat`

Submit a query and get an AI-generated answer.

**Request:**
```json
{
  "message": "What are the admission requirements for CS?"
}
```

**Response:**
```json
{
  "response": "The admission requirements for Computer Science include...",
  "processing_time": 3.45,
  "status": "success"
}
```

**Error Response:**
```json
{
  "detail": "Message cannot be empty"
}
```

### Interactive Documentation

Once the API is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

## 📊 Performance

### Benchmarks

| Metric | Value | Notes |
|--------|-------|-------|
| **Response Time** | 3-5 seconds | End-to-end user experience |
| **Query Expansion** | <50ms | Pure Python operations |
| **Embedding Generation** | 100-200ms | Per query variant (4 total) |
| **Vector Search** | 50-100ms | ChromaDB with HNSW |
| **Reranking** | <50ms | Lightweight scoring |
| **LLM Generation** | 2-4 seconds | Context-dependent |
| **Throughput** | 10-20 queries/min | On 8GB RAM, 4 cores |

### Accuracy

- **Retrieval Recall**: ~85% (finds relevant chunks)
- **Answer Accuracy**: High (grounded in retrieved context)
- **Hallucination Rate**: Very low (temperature=0, context-only)

### Resource Usage

- **RAM**: ~2GB during operation
- **Storage**: ~500MB for vector database
- **CPU**: 30-50% during inference (4 cores)

## 🛠️ Troubleshooting

### Common Issues

#### 1. "Ollama not found"

**Solution:**
```bash
# Check if Ollama is installed
ollama --version

# If not, install it
curl -fsSL https://ollama.ai/install.sh | sh
```

#### 2. "Model not found: gemma3"

**Solution:**
```bash
ollama pull gemma3
ollama pull nomic-embed-text
```

#### 3. "Cannot connect to API"

**Solution:**
- Ensure `python main.py` is running
- Check port 8000 is not in use: `lsof -i :8000`
- Try accessing http://localhost:8000 directly

#### 4. "No relevant information found"

**Possible causes:**
- Query not related to UET prospectus
- Data not ingested (run `python ingest.py`)
- PDF file missing in `data/` directory

**Solution:**
```bash
# Re-run ingestion
python ingest.py
```

#### 5. Slow responses

**Solutions:**
- Reduce `TOP_K_DOCUMENTS` from 6 to 4
- Decrease `MMR_FETCH_K` from 15 to 10
- Use a faster machine or GPU

#### 6. Out of Memory

**Solutions:**
- Reduce `CHUNK_SIZE` to 600
- Lower `MMR_FETCH_K` to 10
- Close other applications
- Upgrade RAM to 16GB

### Debug Mode

Enable detailed logging:

```python
# In agent.py, enable verbose output
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Bugs

1. Check existing [issues](https://github.com/faiwasaeed/uet-rag-system/issues) first
2. Create a new issue with:
   - Clear title and description
   - Steps to reproduce
   - Expected vs actual behavior
   - System information (OS, Python version)

### Suggesting Features

1. Open an [issue](https://github.com/faiwasaeed/uet-rag-system/issues) with tag `enhancement`
2. Describe the feature and use case
3. Explain why it would be useful

### Pull Requests

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Add tests if applicable
5. Commit: `git commit -m 'Add amazing feature'`
6. Push: `git push origin feature/amazing-feature`
7. Open a Pull Request

### Development Setup

```bash
# Clone your fork
git clone https://github.com/faiwasaeed/uet-rag-system.git
cd uet-rag-system

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install in development mode
pip install -r requirements.txt

# Run tests
python agent.py
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2026 Faiza Saeed

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 🙏 Acknowledgments

### Technologies

- **[Ollama](https://ollama.ai/)**: Local LLM inference platform
- **[LangChain](https://langchain.com/)**: RAG framework
- **[ChromaDB](https://www.trychroma.com/)**: Vector database
- **[FastAPI](https://fastapi.tiangolo.com/)**: Modern web framework
- **[Streamlit](https://streamlit.io/)**: Data app framework

### Inspiration

This project demonstrates practical RAG implementation for educational institutions. Special thanks to the open-source AI community for making these tools accessible.

## 📮 Contact

- **GitHub**: [@faiwasaeed](https://github.com/faiwasaeed)
- **Email**: faizasaeed91@gmail.com
- **Project Link**: [https://github.com/faiwasaeed/uet-rag-system](https://github.com/faiwasaeed/uet-rag-system)

## 🗺️ Roadmap

### Version 2.0 (Current)

- ✅ Enhanced query expansion with multi-variant generation
- ✅ Custom reranking algorithm
- ✅ MMR retrieval for diverse results
- ✅ Rich metadata system
- ✅ Streamlit web interface
- ✅ FastAPI backend with documentation

### Version 2.1 (Planned)

- [ ] Multi-document support (multiple prospectuses)
- [ ] Conversation memory for follow-up questions
- [ ] Advanced filters (department, program, year)
- [ ] Query autocomplete and suggestions
- [ ] Answer caching for common queries
- [ ] Multi-language support (Urdu)

### Version 3.0 (Future)

- [ ] Fine-tuned embeddings for UET domain
- [ ] Table and chart extraction from PDF
- [ ] Mobile app (React Native)
- [ ] Voice query support
- [ ] Analytics dashboard
- [ ] Admin panel for content management

---

<div align="center">

**Made with ❤️ for UET students and faculty**

⭐ Star this repo if you find it helpful!


</div>
