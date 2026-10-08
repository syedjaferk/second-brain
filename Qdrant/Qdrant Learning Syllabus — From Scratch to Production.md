---
layout: post
title: Qdrant Learning Syllabus — From Scratch to Production
date: 2026-09-05 18:26
render_with_liquid: false
category: Vector Database
tags:
  - vector
  - embeddings
  - Database
---



## Phase 0: Prerequisites & Conceptual Foundations (3–5 days)

_Goal: Understand why vector databases exist before touching Qdrant itself._

- [x]  What embeddings are (text/image/audio → dense vectors) and how similarity search works (cosine, dot product, Euclidean distance)
- [x]  Difference between exact nearest neighbor (kNN) and approximate nearest neighbor (ANN)
- [ ]  HNSW (Hierarchical Navigable Small World) algorithm — conceptual understanding, not implementation
- [ ]  Where vector DBs fit in an AI stack: embedding models → vector DB → retrieval → LLM (RAG pattern)
- [ ]  Landscape context: how Qdrant compares to Pinecone, Weaviate, Milvus, pgvector, Chroma (know the trade-offs, not just Qdrant in isolation)

## Phase 1: Qdrant Fundamentals (Week 1)

### 1.1 Setup & Deployment Basics

- [ ]  Install via Docker (`docker run qdrant/qdrant`), local binary, and Qdrant Cloud free tier
- [ ]  Qdrant Web UI dashboard — explore collections visually
- [ ]  REST API vs gRPC API — when to use which
- [ ]  Client SDKs overview (Python, JS/TS, Go, Rust, Java) — pick Python as primary if doing RAG/ML work

### 1.2 Core Concepts

- [ ]  Collections, points, vectors, payloads (metadata)
- [ ]  Point IDs (UUID vs integer)
- [ ]  Distance metrics: Cosine, Dot, Euclidean, Manhattan — when each applies
- [ ]  Named vectors / multivectors (storing multiple embeddings per point — e.g., text + image)

### 1.3 Basic CRUD

- [ ]  Create/delete collections, define vector params
- [ ]  Upsert points (single and batch)
- [ ]  Retrieve by ID, delete points
- [ ]  Basic search queries with `limit`, `score_threshold`

## Phase 2: Search & Filtering (Week 2)

- [ ]  Payload schema design — flat vs nested metadata
- [ ]  Filtering: `must`, `should`, `must_not`, range filters, geo filters, full-text match filters
- [ ]  Payload indexing for filter performance (keyword, integer, geo, text indexes)
- [ ]  Pagination: `offset`, `scroll` API for large result sets
- [ ]  Faceting — aggregating results by payload field
- [ ]  Grouping (`query_groups`) — e.g., top-N per category
- [ ]  Sparse vectors and hybrid search (dense + sparse via BM25/SPLADE-style scoring, RRF and DBSF fusion)
- [ ]  Recommendation API (positive/negative example points)
- [ ]  Discovery API (constraining search to a region of vector space using context pairs)
- [ ]  Relevance tuning: Maximal Marginal Relevance (MMR), Relevance Feedback queries (Qdrant 1.17+ feature)

## Phase 3: Building a Real Application (Week 3)

- [ ]  Pick an embedding model (OpenAI, Cohere, or open-source via `sentence-transformers`/FastEmbed)
- [ ]  Qdrant's built-in FastEmbed integration for local, no-API-key embedding generation
- [ ]  Build an end-to-end RAG pipeline: document chunking → embed → upsert with payload (source, chunk index, doc id) → query-time retrieval → pass to LLM
- [ ]  Multitenancy patterns — isolating data per user/tenant within one collection (payload-based partitioning vs separate collections)
- [ ]  Update strategies: upserting changed documents, handling deletes, versioning

## Phase 4: Performance & Storage Internals (Week 4)

- [ ]  HNSW index tuning: `m`, `ef_construct`, `ef` (search-time) parameters and their trade-offs
- [ ]  Quantization: Scalar, Product, and Binary quantization — memory savings vs recall trade-offs (binary quantization can give up to ~40x memory reduction)
- [ ]  On-disk vs in-memory storage (`on_disk` payload/vector options) — memory-mapped storage for large collections
- [ ]  Segment architecture and optimizers (indexing thresholds, segment merging)
- [ ]  Benchmarking: measuring recall, latency (p50/p95/p99), and throughput under load
- [ ]  Choosing vector precision (float32 vs float16 vs uint8)

## Phase 5: Scaling & Distributed Operation (Week 5–6)

- [ ]  Single-node limits — when you need to scale out
- [ ]  Sharding: distributing a collection across nodes
- [ ]  Replication for high availability
- [ ]  Consistency levels for reads/writes
- [ ]  Cluster setup (self-hosted, Raft-based consensus for cluster state)
- [ ]  Snapshotting and backup/restore procedures
- [ ]  Zero-downtime collection migrations and re-indexing strategies
- [ ]  Multi-AZ deployment patterns (if using Qdrant Cloud) for failover without downtime

## Phase 6: Production Readiness (Week 6–7)

- [ ]  Security: API key auth, TLS, role-based access control (RBAC) if on Cloud/Enterprise
- [ ]  Observability: Prometheus metrics integration, per-collection metrics, audit logging, telemetry API
- [ ]  Resource management: memory sizing calculations (vectors × dimensions × bytes-per-value + overhead), CPU sizing for indexing vs querying
- [ ]  Rate limiting & quotas: protecting cluster from noisy-neighbor issues (global quota APIs)
- [ ]  Deployment strategies: Docker Compose for small setups, Kubernetes (Helm chart) for scale, Qdrant Cloud managed vs self-hosted vs hybrid vs private deployment trade-offs
- [ ]  CI/CD: automating collection schema migrations, testing embedding pipeline changes
- [ ]  Cost optimization: quantization + on-disk storage to reduce cluster size; GPU-accelerated indexing for large bulk-loading jobs

## Phase 7: Advanced Topics & Specialization (Week 7–8+)

- [ ]  Building hybrid search systems combining keyword (BM25/sparse) + semantic (dense) retrieval well
- [ ]  Re-ranking pipelines (cross-encoders after Qdrant's initial retrieval)
- [ ]  Multi-modal search (text-to-image, image-to-image) using named vectors
- [ ]  Integrating Qdrant with LangChain, LlamaIndex, Haystack for RAG frameworks
- [ ]  A/B testing different embedding models on the same dataset
- [ ]  Disaster recovery drills and chaos-testing a cluster
- [ ]  Contributing to or reading Qdrant's Rust source for deep internals (optional)



---

## Related Posts
- [[]]
- [[]]
