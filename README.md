# Enterprise IT Support — Agentic RAG Copilot

A learning and development project exploring how Retrieval-Augmented Generation (RAG) and AI agents can support enterprise IT help desks by answering questions from internal knowledge documents and using web search when additional information is needed.

> **Project status:** Learning, setup, and testing in progress. This repository is a fork of the original project. I am using it to understand the architecture, run the application, validate its workflows, and develop my own improvements.

## Problem Statement

IT support teams repeatedly answer questions about VPN access, account security, software installation, and troubleshooting. Finding the correct information across multiple documents can be time-consuming.

This project explores an AI-powered assistant that can:

- Retrieve relevant information from an internal IT knowledge base.
- Generate answers grounded in retrieved documents.
- Evaluate whether the available information is sufficient.
- Use web search when internal knowledge does not provide an adequate answer.
- Display the reasoning path followed by the workflow for easier debugging.

## How It Works

**Question → Routing → Knowledge Retrieval → Evidence Evaluation → Answer Generation**

1. A user submits an IT support question.
2. The workflow determines whether the message requires knowledge retrieval.
3. Relevant passages are retrieved from the internal knowledge base.
4. The workflow evaluates whether the retrieved evidence is sufficient.
5. If necessary, it can use web search or retry with a revised query.
6. The assistant generates an answer based on the available evidence.

## Technology Stack

- **Language:** Python
- **Backend:** FastAPI
- **Agent orchestration:** LangGraph
- **LLM integration:** Groq
- **Embeddings:** Sentence Transformers / configured embedding provider
- **Vector database:** Pinecone
- **Web search:** Tavily
- **Frontend:** HTML, CSS, JavaScript
- **Audit logging:** SQLite
- **Packaging:** Docker

These are the technologies documented by the upstream project. Their successful configuration and execution in my environment remain part of the validation process.

## Project Setup

### Prerequisites

- Python installed
- Git installed
- A code editor such as VS Code
- API credentials for the external services required by the configured application

### 1. Clone the repository

```bash
git clone https://github.com/RitikaSaha14/Enterprise-IT-Support-Agentic-RAG-Copilot.git
cd Enterprise-IT-Support-Agentic-RAG-Copilot
```

### 2. Create a virtual environment

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file in the project root using `.env.example` as a reference. Add the credentials required by the application.

Typical variables documented by the upstream project include:

```text
GROQ_API_KEY=
OPENAI_API_KEY=
TAVILY_API_KEY=
PINECONE_API_KEY=
PINECONE_INDEX_NAME=fde-it-support-rag
PINECONE_NAMESPACE=company-it-kb
ADMIN_API_KEY=
APP_ENV=development
```

Check the current configuration and source code to confirm which variables are required by the version you are running. Never commit `.env` or expose API keys in source code, screenshots, or logs.

### 5. Load the sample knowledge base

```bash
python ingest_sample_kb.py
```

This step is intended to load and index the sample IT documents. Confirm that it completes successfully before proceeding.

### 6. Run the application

```bash
python run.py
```

If startup succeeds, open:

- Application: http://127.0.0.1:8000
- API documentation: http://127.0.0.1:8000/docs

If a command fails, record the error and investigate the relevant configuration or dependency before treating the application as operational.

## Testing Plan

I will validate the following scenarios as I work through the implementation.

| Test | Example question | Expected behavior |
|---|---|---|
| Internal knowledge retrieval | How do I connect to the company VPN from home? | Retrieve relevant internal guidance and answer from it. |
| Security policy | Should I share my MFA code with IT support? | Return the relevant security policy. |
| Web-search fallback | What is the latest Microsoft Teams outage guidance? | Use external search if internal evidence is insufficient. |
| Vague query | My work communication app is acting strangely. What should I do? | Evaluate retrieval quality and retry when appropriate. |
| Greeting | Hello! | Respond without unnecessary document retrieval. |
| Health check | Call `GET /api/health` | Return the application's health response. |

These are planned test cases, not claims that all tests have passed. I will record the actual results as I execute them.

## Current Development Checklist

- [ ] Set up the Python environment.
- [ ] Install and validate dependencies.
- [ ] Configure API credentials securely.
- [ ] Run sample knowledge-base ingestion.
- [ ] Start the FastAPI application.
- [ ] Test internal document retrieval.
- [ ] Test evidence evaluation and web-search fallback.
- [ ] Verify API responses and source information.
- [ ] Review error handling and audit logs.
- [ ] Run available tests and document the results.
- [ ] Identify and implement original improvements.
- [ ] Validate Docker packaging and deployment, if feasible.

## Learning Objectives

Through this project, I aim to strengthen my understanding of:

- RAG pipelines, document chunking, embeddings, and semantic retrieval.
- Vector databases and knowledge-base integration.
- LangGraph state management and conditional workflows.
- FastAPI endpoints and external API integration.
- Retrieval quality, grounded responses, and error handling.
- Testing, logging, and secure environment configuration.

## Development Goals

- Build and validate an end-to-end Agentic RAG workflow.
- Test document retrieval, evidence evaluation, and web-search fallback.
- Improve error handling, API reliability, and response quality.
- Document test results and implementation improvements.
## Next Steps

The immediate goal is to get the project running locally, understand the end-to-end RAG workflow, validate the documented test scenarios, and then build and document meaningful improvements.
