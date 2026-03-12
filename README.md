# Agentic Retrieval-Augmented E-Commerce Product Assistant

Python LangChain LangGraph AstraDB FastAPI Streamlit

Overview

ProductRAG is an Agentic Retrieval-Augmented Generation (RAG) system designed for intelligent e-commerce product search and recommendation.

The system:

Scrapes product information and reviews from Flipkart

Converts reviews into vector embeddings

Stores embeddings inside AstraDB Vector Store

Uses a LangGraph agentic workflow to retrieve and reason over product data

Provides a chatbot capable of answering complex product queries

Example questions:

- Suggest a good iPhone under ₹50,000
- Which phone has the best camera?
- Compare iPhone 13 and iPhone 14
- Best rated smartphone under ₹30,000

## Key Features

- Flipkart product scraping
- Automated product review ingestion
- Vector database storage using AstraDB
- Semantic product search
- Agentic RAG pipeline using LangGraph
- Web fallback search using MCP tools
- Chatbot interface using FastAPI
- Scraper UI using Streamlit
- CI/CD deployment to AWS EKS

## System Architecture

```
User Query
     │
     ▼
Agentic Workflow (LangGraph)
     │
     ├── Vector Retrieval (AstraDB)
     │
     ├── Query Rewriting
     │
     ├── Document Relevance Grading
     │
     └── MCP Tool Invocation (Web Search)
           │
           ▼
        LLM Response
```

## Data Pipeline

```
Flipkart Scraper
       │
       ▼
CSV Dataset
(product_reviews.csv)
       │
       ▼
LangChain Documents
       │
       ▼
Embedding Generation
       │
       ▼
AstraDB Vector Store
       │
       ▼
Retriever + Compression
       │
       ▼
Chatbot Response
```

## Repository Structure

```
ProductRAG
│
├── prod_assistant
│   │
│   ├── config
│   │   └── config.yaml
│   │
│   ├── etl
│   │   ├── data_scrapper.py
│   │   └── data_injection.py
│   │
│   ├── retriever
│   │   └── retrieval.py
│   │
│   ├── workflow
│   │   ├── agentic_workflow.py
│   │   └── agentic_workflow_with_mcp.py
│   │
│   ├── router
│   │   └── main.py
│   │
│   ├── mcp_servers
│   │   ├── client.py
│   │   └── server.py
│   │
│   ├── utils
│   │   ├── model_loader.py
│   │   └── config_loader.py
│   │
│   └── prompt_library
│       └── prompts.py
│
├── templates
│
├── static
│
├── notebook
│
├── scrapper_ui.py
│
├── requirements.txt
│
├── dockerfile
│
└── README.md
```

## Technology Stack

| Component          | Technology                  |
|--------------------|-----------------------------|
| Language           | Python                      |
| Framework          | LangChain                   |
| Agent Workflow     | LangGraph                   |
| Vector Database    | AstraDB                     |
| Backend API        | FastAPI                     |
| Scraper UI         | Streamlit                   |
| Web Scraping       | Selenium + BeautifulSoup    |
| LLM Providers      | OpenAI / Google / Groq      |
| Evaluation         | Ragas                       |
| Tool Integration   | MCP                         |

## Installation

### Clone the repository

```bash
git clone https://github.com/amitkumar981/e_commerce-chatbot.git
cd e_commerce-chatbot
```

### Create virtual environment

```bash
python -m venv .venv
```

### Activate environment

**Windows**

```bash
.venv\Scripts\activate
```

**Linux / macOS**

```bash
source .venv/bin/activate
```

### Install dependencies

```bash
pip install -r requirements.txt
pip install -e .
```

## Environment Variables

Create a `.env` file in the root directory.

```env
OPENAI_API_KEY=your_openai_key
GOOGLE_API_KEY=your_google_key
GROQ_API_KEY=your_groq_key

ASTRA_DB_API_ENDPOINT=your_endpoint
ASTRA_DB_APPLICATION_TOKEN=your_token
ASTRA_DB_KEYSPACE=your_keyspace
```

## Running the Project

### Run Scraper UI

```bash
streamlit run scrapper_ui.py
```

This allows you to:

- search products
- scrape reviews
- export CSV
- ingest data to vector database

### Run Chatbot API

```bash
uvicorn prod_assistant.router.main:app --reload --port 8005
```

Open your browser to interact with the chatbot.

## Docker Deployment

**Build image**

```bash
docker build -t productrag .
```

**Run container**

```bash
docker run -p 8005:8005 --env-file .env productrag
```

This launches:

- MCP server
- FastAPI chatbot service
- CI/CD Pipeline

## CI/CD & Infrastructure

The project uses GitHub Actions for automated infrastructure provisioning and application deployment.

### Infrastructure Workflow (`infra.yml`)

**Purpose:** Provision AWS infrastructure using CloudFormation.

**Resources created:**

- Amazon EKS cluster
- Amazon ECR repository
- Networking components

**Trigger:** `workflow_dispatch` (manual)

### Deployment Workflow (`deploy.yml`)

**Triggered on:**

- Push to `main`
- Manual dispatch

**Pipeline steps:**

1. Checkout repository
2. Configure AWS credentials
3. Verify EKS cluster
4. Login to Amazon ECR
5. Build Docker image
6. Push image to ECR
7. Update Kubernetes deployment
8. Wait for rollout completion
9. Output service details

**Deployment target:** Amazon EKS

## Example Queries

- Suggest a good iPhone under 50000
- Which phone has the best camera
- Compare iPhone 13 and iPhone 14
- Best smartphone under 30000 with high rating

## Future Improvements

- Multi-platform scraping (Amazon / Myntra)
- Hybrid search with metadata filtering
- Product ranking models
- Monitoring and observability
- Production-grade CI/CD environments
- Caching and latency optimization

## Author

**Amit Kumar**  
Machine Learning Engineer

**Focus:**

- Retrieval Augmented Generation (RAG)
- AI Agents
- Production ML Systems
- LLM Infrastructure










