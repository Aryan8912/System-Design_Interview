# Designing a Production RAG System with Multi-Agent Orchestration

This article explores designing and implementing a production-grade Retrieval-Augmented Generation (RAG) system using Python.

The architecture includes:

* document ingestion
* OCR
* chunking
* embeddings
* vector retrieval
* reranking
* multi-agent orchestration
* caching
* async inference
* vLLM serving
* LangGraph-style execution

---

# System Requirements

The RAG platform should support:

* Document Ingestion
  Upload PDFs, scanned documents, webpages, and text files.

* OCR Processing
  Extract text from scanned PDFs and images.

* Chunking + Embedding
  Split documents into semantic chunks and generate embeddings.

* Hybrid Retrieval
  Support both vector retrieval and keyword retrieval.

* Reranking
  Improve retrieval precision using cross-encoder rerankers.

* Multi-Agent Reasoning
  Use planner, retriever, reasoning, and verifier agents.

* Async Inference APIs
  Handle thousands of concurrent users.

* Caching
  Use Redis for semantic caching and retrieval caching.

* Streaming Responses
  Stream tokens from the LLM in real time.

* Citation Generation
  Return grounded responses with document references.

---

# Core Use Cases

* Uploading enterprise documents
* Asking questions from documents
* Multi-step reasoning over retrieved context
* Generating grounded answers
* Streaming LLM responses
* Agent orchestration
* Retrieval optimization
* Hallucination reduction

---

# High-Level Architecture

```text id="jlwm9a"
User Query
    ↓
FastAPI Gateway
    ↓
Planner Agent
    ↓
Retriever Agent
    ↓
Hybrid Retrieval
    ↓
Reranker Agent
    ↓
Reasoning Agent
    ↓
Verifier Agent
    ↓
vLLM Inference Server
    ↓
Streaming Response
```

Document pipeline:

```text id="jlwme2"
PDF → OCR → Chunking → Embeddings → Vector DB
```

---

# Key Classes

| Class               | Responsibility           |
| ------------------- | ------------------------ |
| RAGSystem           | Main orchestration       |
| DocumentProcessor   | OCR + parsing            |
| Chunker             | Semantic chunking        |
| EmbeddingService    | Generate embeddings      |
| VectorDatabase      | ANN retrieval            |
| RetrieverAgent      | Retrieve relevant chunks |
| RerankerAgent       | Rank retrieved chunks    |
| PlannerAgent        | Task decomposition       |
| ReasoningAgent      | Generate final answer    |
| VerifierAgent       | Validate grounding       |
| CacheManager        | Redis caching            |
| vLLMEngine          | LLM inference            |
| AsyncInferenceQueue | Request batching         |

---

# Python Implementation

```python
import asyncio
from typing import List, Dict
import numpy as np

# -----------------------------
# Document Class
# -----------------------------

class Document:
    def __init__(self, doc_id: str, content: str):
        self.doc_id = doc_id
        self.content = content


# -----------------------------
# Chunk Class
# -----------------------------

class Chunk:
    def __init__(self, chunk_id: str, text: str, metadata: Dict):
        self.chunk_id = chunk_id
        self.text = text
        self.metadata = metadata


# -----------------------------
# OCR + Document Processing
# -----------------------------

class DocumentProcessor:

    async def extract_text(self, file_path: str) -> str:
        print(f"OCR processing: {file_path}")

        # Simulated OCR extraction
        await asyncio.sleep(1)

        return "Extracted document text"


# -----------------------------
# Chunking Service
# -----------------------------

class Chunker:

    def chunk_document(self, text: str) -> List[Chunk]:

        chunks = []

        chunk_size = 100

        for i in range(0, len(text), chunk_size):

            chunk_text = text[i:i + chunk_size]

            chunks.append(
                Chunk(
                    chunk_id=f"chunk_{i}",
                    text=chunk_text,
                    metadata={"position": i}
                )
            )

        return chunks


# -----------------------------
# Embedding Service
# -----------------------------

class EmbeddingService:

    async def generate_embedding(self, text: str):

        await asyncio.sleep(0.1)

        # Fake embedding vector
        return np.random.rand(768)


# -----------------------------
# Vector Database
# -----------------------------

class VectorDatabase:

    def __init__(self):
        self.index = []

    def add_embedding(self, chunk: Chunk, embedding):

        self.index.append({
            "chunk": chunk,
            "embedding": embedding
        })

    async def search(self, query_embedding, top_k=5):

        await asyncio.sleep(0.2)

        return self.index[:top_k]


# -----------------------------
# Hybrid Retriever
# -----------------------------

class RetrieverAgent:

    def __init__(self, vector_db: VectorDatabase):
        self.vector_db = vector_db

    async def retrieve(self, query_embedding):

        print("Retriever Agent Running")

        results = await self.vector_db.search(query_embedding)

        return results


# -----------------------------
# Reranker Agent
# -----------------------------

class RerankerAgent:

    async def rerank(self, query: str, retrieved_chunks):

        print("Reranking Retrieved Chunks")

        await asyncio.sleep(0.1)

        return retrieved_chunks


# -----------------------------
# Planner Agent
# -----------------------------

class PlannerAgent:

    async def plan(self, query: str):

        print("Planner Agent Creating Plan")

        await asyncio.sleep(0.1)

        return {
            "retrieve": True,
            "verify": True
        }


# -----------------------------
# Reasoning Agent
# -----------------------------

class ReasoningAgent:

    async def reason(self, query, context):

        print("Reasoning Agent Generating Answer")

        await asyncio.sleep(0.2)

        return f"Generated answer for: {query}"


# -----------------------------
# Verifier Agent
# -----------------------------

class VerifierAgent:

    async def verify(self, answer, retrieved_chunks):

        print("Verifier Agent Checking Grounding")

        await asyncio.sleep(0.1)

        return True


# -----------------------------
# Redis Cache Manager
# -----------------------------

class CacheManager:

    def __init__(self):
        self.cache = {}

    def get(self, key):

        return self.cache.get(key)

    def set(self, key, value):

        self.cache[key] = value


# -----------------------------
# vLLM Inference Engine
# -----------------------------

class vLLMEngine:

    async def generate(self, prompt):

        print("vLLM Generating Tokens")

        await asyncio.sleep(1)

        return "LLM generated response"


# -----------------------------
# Async Inference Queue
# -----------------------------

class AsyncInferenceQueue:

    def __init__(self):
        self.queue = asyncio.Queue()

    async def add_request(self, request):

        await self.queue.put(request)

    async def process_requests(self):

        while True:

            request = await self.queue.get()

            print(f"Processing request: {request}")

            await asyncio.sleep(0.5)


# -----------------------------
# LangGraph-style Orchestrator
# -----------------------------

class RAGSystem:

    def __init__(self):

        self.processor = DocumentProcessor()

        self.chunker = Chunker()

        self.embedding_service = EmbeddingService()

        self.vector_db = VectorDatabase()

        self.retriever = RetrieverAgent(self.vector_db)

        self.reranker = RerankerAgent()

        self.planner = PlannerAgent()

        self.reasoner = ReasoningAgent()

        self.verifier = VerifierAgent()

        self.cache = CacheManager()

        self.llm = vLLMEngine()

    # -------------------------
    # Document Ingestion
    # -------------------------

    async def ingest_document(self, file_path):

        text = await self.processor.extract_text(file_path)

        chunks = self.chunker.chunk_document(text)

        for chunk in chunks:

            embedding = await self.embedding_service.generate_embedding(chunk.text)

            self.vector_db.add_embedding(chunk, embedding)

        print("Document ingestion completed")

    # -------------------------
    # Query Pipeline
    # -------------------------

    async def query(self, user_query):

        # Cache Lookup
        cached_response = self.cache.get(user_query)

        if cached_response:
            print("Cache Hit")
            return cached_response

        # Planner Agent
        plan = await self.planner.plan(user_query)

        # Query Embedding
        query_embedding = await self.embedding_service.generate_embedding(user_query)

        # Retrieval
        retrieved_chunks = await self.retriever.retrieve(query_embedding)

        # Reranking
        reranked_chunks = await self.reranker.rerank(
            user_query,
            retrieved_chunks
        )

        # Reasoning
        answer = await self.reasoner.reason(
            user_query,
            reranked_chunks
        )

        # Verification
        verified = await self.verifier.verify(
            answer,
            reranked_chunks
        )

        if not verified:
            return "Verification failed"

        # LLM Generation
        final_response = await self.llm.generate(answer)

        # Cache Result
        self.cache.set(user_query, final_response)

        return final_response


# -----------------------------
# Main Execution
# -----------------------------

async def main():

    rag = RAGSystem()

    # Ingest documents
    await rag.ingest_document("enterprise_report.pdf")

    # User Query
    response = await rag.query(
        "What are the Q3 revenue risks?"
    )

    print("\nFinal Response:")
    print(response)


if __name__ == "__main__":
    asyncio.run(main())
```

---

# Execution Flow

```text id="jlwmd4"
PDF Upload
    ↓
OCR Extraction
    ↓
Chunking
    ↓
Embedding Generation
    ↓
Vector DB Storage
    ↓
User Query
    ↓
Planner Agent
    ↓
Retriever Agent
    ↓
Hybrid Retrieval
    ↓
Reranker Agent
    ↓
Reasoning Agent
    ↓
Verifier Agent
    ↓
vLLM Generation
    ↓
Streaming Response
```

---

# Production Optimizations

---

# 1. Retrieval Optimization

Use:

* HNSW indexing
* hybrid retrieval
* metadata filtering
* ANN search

---

# 2. GPU Inference Optimization

Use:

* continuous batching
* paged attention
* prefix caching
* quantization

with:
vLLM

---

# 3. Hallucination Reduction

Use:

* reranking
* verifier agents
* citation grounding
* contextual compression

---

# 4. Async Concurrency

Use:

* async FastAPI
* asyncio queues
* SSE token streaming

---

# 5. Multi-Agent Orchestration

Use:
LangGraph
for:

* planner
* retriever
* verifier
* reasoning agents

---

# 6. Observability

Monitor:

* Recall@K
* latency
* hallucination rate
* GPU utilization
* cache hit rate

Using:

* Prometheus
* Grafana
* LangSmith

---

# Final Architecture Summary

```text id="jlwmt3"
Frontend
   ↓
FastAPI Gateway
   ↓
LangGraph Orchestrator
   ↓
Planner Agent
   ↓
Retriever Agent
   ↓
Hybrid Retrieval
   ↓
Reranker Agent
   ↓
Reasoning Agent
   ↓
Verifier Agent
   ↓
vLLM Inference Cluster
   ↓
Streaming Response
```
