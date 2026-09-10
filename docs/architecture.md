## Architecture

```text
User
  |
  v
React + Vite multilingual interface
  |
  v
FastAPI API Gateway
  |
  v
Orchestrator Service
  |
  +--> Query Router (conceptual / legal / hybrid)
  |       |
  |       +--> RAG 1: Ayurveda and traditional-knowledge retrieval
  |       |
  |       +--> RAG 2: Legal and regulatory evidence retrieval
  |
  +--> Citation ranking, conflict detection, and evidence fusion
  |
  v
Groq LLM guardrailed synthesis
  |
  v
Source-cited response + confidence score + optional human escalation
```

The application keeps the RAG 1 and RAG 2 stores separate (`vector.db` and `vector_rag2.db`). The legal corpus preserves source metadata and is versioned to support traceability.


## Components

### Frontend
React-based interface for user queries, multilingual interaction, citations, confidence scores, and human-review escalation.

### Backend API
FastAPI backend that handles requests and coordinates multilingual processing, RAG retrieval, response generation, and escalation.

### AI / RAG System
Two RAG pipelines:
- RAG 1: Ayurveda, Traditional Knowledge, and IP knowledge
- RAG 2: Legal and Regulatory evidence

An LLM generates grounded responses using the retrieved evidence.

### Data Storage
Vector databases store RAG knowledge and evidence, while escalation records are stored for human IP-facilitator review.

### Data Flow
User → Frontend → FastAPI Backend → Multi-RAG Retrieval → LLM → Citations + Confidence → Response / Human Escalation