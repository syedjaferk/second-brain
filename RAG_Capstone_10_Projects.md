# RAG Capstone Project Flow
### Based on: `40-day-rag-parottasalna` (syedjaferk)

The repo's 29 modules progress from fundamentals (vector DBs, chunking, embeddings) through
production concerns (caching, reranking, agentic RAG, multi-agent, MCP, memory) to
production-hardening (evaluation, hallucination detection, guardrails, load testing).

Below are **10 capstone projects**, sequenced so each one builds directly on the modules and
skills of the one before it. By Project 10, a learner will have built one evolving RAG
system that started as a toy notebook and ends as a load-tested, guardrailed, evaluated
production service.

---

## Project 1 — "PDF Buddy": Your First Retrieval-Augmented Q&A Bot
**Maps to modules:** `02.need_of_vector_db`, `03.chunking`, `04.embedding`, `05.simple_rag`

### Description
Build the simplest possible end-to-end RAG pipeline. The learner ingests a small set of
PDFs/text files, chunks them, embeds the chunks, stores them in a vector database, and
answers user questions by retrieving the top-k chunks and stuffing them into an LLM prompt.
The goal isn't sophistication — it's *feeling* why a vector DB and chunking strategy matter,
by deliberately trying bad chunk sizes/overlaps and bad `k` values and observing broken answers.

### What the learner must do
- Ingest 3–5 documents (e.g., a company handbook, a couple of research papers).
- Implement at least two chunking strategies (fixed-size vs. recursive/sentence-aware) and compare answer quality.
- Store embeddings in a vector DB (Chroma/FAISS/Qdrant — any one).
- Build a simple `ask(question)` function: embed query → retrieve top-k → build prompt → call LLM → return answer.

### Inputs
- 3–5 PDF/TXT/Markdown documents (~5–50 pages total).
- A set of 10 test questions (mix of "answerable from docs" and "not in docs" questions).
- Configurable parameters: chunk size, chunk overlap, `k` (number of retrieved chunks), embedding model.

### Expected Output
- A CLI or notebook where a user types a question and gets a grounded answer with the source chunk(s) shown.
- A short comparison report: answer accuracy/relevance across 2 chunking strategies and at least 3 values of `k`.
- A clear demonstration of a failure case (e.g., hallucination when `k` is too low, or irrelevant retrieval when chunks are too large) with an explanation of why it happened.

---

## Project 2 — "Living Docs": Prompt-Engineered RAG with Auto-Updating Knowledge
**Maps to modules:** `06.prompt_engineering`, `07.basic_rag_implementation`, `08.rag_doc_update_theory`

### Description
Extend Project 1 into a proper application-grade RAG implementation with disciplined prompt
engineering (system prompts, few-shot grounding instructions, citation formatting, refusal
behavior) and a document lifecycle: the knowledge base must support adding, updating, and
deleting source documents without a full re-index, and answers must reflect the latest version
of a document (no stale/duplicate chunks).

### What the learner must do
- Design a system prompt that enforces: answer only from context, cite the source, say "I don't know" when context is insufficient.
- Implement an update pipeline: when a document changes, re-chunk only that document, delete its old vectors (by document ID/metadata), and insert the new ones.
- Add a simple ingestion API/CLI: `add_doc()`, `update_doc()`, `delete_doc()`.
- Write at least 5 prompt variants and A/B test them against a fixed question set to show measurable improvement.

### Inputs
- The same knowledge base as Project 1, plus a "v2" edited version of at least 2 documents (to test updates).
- A set of "trick" questions designed to test refusal behavior (questions with no answer in the docs).
- Prompt templates to compare.

### Expected Output
- A working `add/update/delete` document API that keeps the vector store consistent (no orphaned or duplicate chunks — verifiable by inspecting the DB).
- Side-by-side answers before/after a document update, proving the system uses the newest version.
- A short write-up: which prompt template performed best and why, with example outputs of correct refusals vs. hallucinations.

---

## Project 3 — "No-Code RAG Ops": Automating Ingestion & Retrieval with n8n
**Maps to modules:** `09.n8n`, `10.rag_with_n8n`

### Description
Take the RAG pipeline out of pure code and rebuild the ingestion and query flow as a visual
workflow in n8n. This teaches learners to think of RAG as a set of orchestrated, observable
steps (webhook → chunk → embed → upsert; and query → embed → retrieve → LLM → respond) that
non-engineers (e.g., ops/content teams) could trigger and monitor.

### What the learner must do
- Build an n8n workflow that watches a folder/Google Drive/webhook for new documents and automatically ingests them into the vector DB from Project 2.
- Build a second n8n workflow exposing a webhook endpoint that accepts a question and returns a RAG answer (calling the vector DB + LLM nodes).
- Add error handling/notification nodes (e.g., Slack/email alert if ingestion fails).

### Inputs
- A shared folder or Google Drive location with new/updated documents dropped in periodically.
- Webhook test requests (via Postman/curl) simulating user questions.
- Credentials/config for the vector DB and LLM API used in n8n nodes.

### Expected Output
- Two working, exportable n8n workflow JSON files: one for automated ingestion, one for query-answering.
- A demo: drop a new file into the watched folder and, without touching code, see it become queryable within the workflow.
- A short architecture diagram showing how n8n replaces the manual scripts from Projects 1–2.

---

## Project 4 — "Smart Filter Search": Metadata-Filtered, Reranked Enterprise Search
**Maps to modules:** `11.metadata_filtering`, `12.Reranking`

### Description
Simulate a multi-tenant / multi-category enterprise document repository (e.g., HR docs, Legal
docs, Engineering docs, tagged by department, date, and access level). The learner builds
retrieval that first narrows candidates using metadata filters, then reranks the filtered
candidates with a cross-encoder or reranking model to push the truly best chunk to the top —
directly addressing the precision limits of pure vector similarity.

### What the learner must do
- Tag every ingested chunk with metadata: `department`, `doc_type`, `created_date`, `access_level`.
- Implement filtered retrieval: e.g., "only search Legal docs created after 2023 that this user's role can access."
- Add a reranking step (e.g., cross-encoder model or LLM-based reranker) on top of the filtered vector search results.
- Compare answer quality/precision with vs. without metadata filtering, and with vs. without reranking.

### Inputs
- A synthetic multi-department document set (at least 4 categories, 5+ docs each) with metadata attached.
- A set of user "personas" with different access levels/department scopes.
- 15+ test queries, several deliberately ambiguous (answerable correctly only if filtered properly).

### Expected Output
- A retrieval function that accepts `(query, user_role, filters)` and returns correctly scoped, reranked results.
- A precision comparison table: top-1/top-3 accuracy for (a) plain vector search, (b) + metadata filtering, (c) + filtering + reranking.
- A demonstrated access-control case: a user without Legal access never sees Legal content, even if it's the best semantic match.

---

## Project 5 — "Fast & Smart Query": Semantic Caching + Query Expansion/Transformation
**Maps to modules:** `13.semantic_caching`, `14.query_expansion_and_transformation`

### Description
Focus on speed and recall. Learners add a semantic cache so near-duplicate questions ("What's
your refund policy?" vs. "How do refunds work?") hit a cache instead of re-running retrieval +
generation, cutting latency and cost. They also implement query expansion/transformation
(e.g., HyDE, multi-query generation, query rewriting for vague/short queries) to improve recall
on poorly-phrased user questions.

### What the learner must do
- Implement a semantic cache: embed incoming queries, check similarity against cached query-answer pairs, return cached answer above a similarity threshold, else run the full pipeline and cache the result.
- Implement at least two query transformation techniques (e.g., HyDE — generate a hypothetical answer and embed that; and multi-query — generate 3 reworded versions of the user's query and merge retrieved results).
- Add cache invalidation logic tied to the document-update pipeline from Project 2 (stale cache entries must be evicted when source docs change).

### Inputs
- A query log/test set with intentional near-duplicates and paraphrases (at least 20 queries, several paraphrase clusters).
- Vague/short queries (e.g., "pricing?") to test whether expansion improves retrieval.
- Latency/cost measurement harness (simple timers/token counters).

### Expected Output
- Benchmarks: average latency and LLM token cost with caching ON vs. OFF across the query log.
- Cache hit-rate report showing correct hits (paraphrases reused) and correct misses (genuinely new questions not incorrectly served stale answers).
- Recall comparison: retrieval quality on vague queries with vs. without query expansion.
- Proof that updating a document correctly invalidates any cached answers that depended on it.

---

## Project 6 — "Deep Retriever": Context Compression, Parent-Document & Multi-Vector Retrieval
**Maps to modules:** `15.context_compression`, `16.parent_retriever`, `17.multivector-retrieval`

### Description
Tackle the "small chunk vs. full context" tension. Learners build a research-assistant style
retriever over long, structured documents (e.g., technical manuals or research papers) using
three advanced strategies: compressing retrieved context to only the relevant sentences before
sending to the LLM, retrieving small child chunks but returning their larger parent chunk/section
for full context, and indexing multiple vector representations per document (e.g., summary +
raw chunk + generated questions) to improve matching.

### What the learner must do
- Implement context compression: after retrieval, use an LLM or extractive method to strip retrieved chunks down to only the sentences relevant to the query before final generation.
- Implement the parent-document retriever pattern: index small chunks for precise matching, but fetch and pass the parent section/document to the LLM.
- Implement multi-vector retrieval: generate and index multiple representations per chunk (e.g., a summary vector and a hypothetical-question vector) and merge retrieval across them.
- Measure token usage and answer quality across all three strategies vs. the Project 1 baseline.

### Inputs
- 3–5 long, hierarchically structured documents (with clear sections/subsections — e.g., a technical manual with headings).
- 15 questions requiring broader context than a single chunk provides (e.g., "summarize section 3" or "what are the tradeoffs discussed in the architecture chapter").

### Expected Output
- A retrieval module supporting all three strategies behind a single interface (`retrieve(query, strategy="compression"|"parent"|"multivector")`).
- A comparison table: context tokens sent to the LLM, answer completeness, and answer accuracy per strategy.
- A written recommendation of which strategy fits which document type/question type, backed by the experiment results.

---

## Project 7 — "Follow-Up Friendly": Multi-Hop Reasoning Conversational RAG Assistant
**Maps to modules:** `18.multi-hop`, `19.conversational-rag`

### Description
Build a chat-style assistant that can (a) hold a multi-turn conversation, correctly resolving
pronouns/follow-ups against prior turns, and (b) answer questions that require chaining multiple
retrieval steps together (multi-hop), where the answer to one sub-question is needed to form the
retrieval query for the next.

### What the learner must do
- Implement conversation memory: rewrite follow-up questions into standalone questions using chat history before retrieval (e.g., "What about its pricing?" → "What is the pricing of Product X?").
- Implement a multi-hop pipeline: decompose a complex question into sub-questions, retrieve and answer each sequentially, then synthesize a final answer using all intermediate results.
- Build a chat UI or CLI loop that maintains session state across turns.

### Inputs
- A knowledge base with genuinely cross-referential facts (e.g., "Company A acquired Company B in 2021; Company B's product X was renamed Y" spread across different documents).
- A scripted multi-turn conversation (8–10 turns) including pronoun references and topic shifts.
- 5 multi-hop questions requiring 2–3 chained retrievals to answer correctly.

### Expected Output
- A transcript demonstrating correct follow-up resolution across the full scripted conversation.
- For each multi-hop question: a visible trace of the sub-questions generated, the intermediate retrieved facts, and the final synthesized answer.
- A failure-case analysis: one example each of a broken follow-up and a broken multi-hop chain, with root cause explained (and, ideally, fixed).

---

## Project 8 — "RAG at Speed": Async, Streaming Production API
**Maps to modules:** `20.async_pipelines`, `21.streaming_rag`

### Description
Turn the assistant into a real backend service. Learners rebuild the retrieval + generation
pipeline using async I/O (so retrieval, reranking, and multiple LLM calls can run concurrently
rather than sequentially) and add token-by-token streaming so the frontend can show the answer
as it's generated instead of waiting for the full response.

### What the learner must do
- Rewrite the pipeline (embedding, vector search, reranking, LLM call) using async/await, and parallelize independent steps (e.g., run multi-query retrieval calls concurrently).
- Expose a streaming HTTP endpoint (e.g., FastAPI with Server-Sent Events or WebSockets) that streams the LLM's answer tokens as they're generated, along with the retrieved sources once known.
- Load a basic frontend (or `curl -N`) to visibly demonstrate streaming output.
- Benchmark latency-to-first-token and total-response-time, sync vs. async.

### Inputs
- The Project 6/7 pipeline as the base to convert.
- A batch of concurrent test requests (e.g., 10 simultaneous questions) to demonstrate async throughput gains.
- A simple client (browser fetch, curl, or minimal HTML page) to visualize streaming.

### Expected Output
- A running FastAPI (or equivalent) service with a `/chat` streaming endpoint and a `/health` endpoint.
- Benchmark results: latency-to-first-token and total throughput for sync vs. async implementations under concurrent load.
- A short demo recording/GIF or description of the token-by-token streaming in the client.

---

## Project 9 — "Agent Team": Agentic, Multi-Agent RAG with MCP Tools & Memory
**Maps to modules:** `22.agentic_rag`, `23.multi-agent-rag`, `24.mcp_rag`, `25.memory_systems`

### Description
The most architecturally ambitious project. Learners convert the RAG assistant into an agentic
system: instead of always retrieving-then-answering, an agent decides *whether* to retrieve,
*what* tool to use (vector search vs. a live API vs. a calculator), and can loop/self-correct.
This is then extended to multiple specialized agents coordinating on a task (e.g., a Researcher
agent + a Writer agent + a Critic agent), tools are exposed via MCP (Model Context Protocol) so
the agent can call external services in a standardized way, and a persistent memory system lets
the agent remember user preferences and past interactions across sessions.

### What the learner must do
- Build a single agent with a reasoning loop (ReAct-style or similar) that chooses between: RAG retrieval, a calculator tool, and a live web-search tool, based on the question.
- Extend to a multi-agent setup: at least 2–3 agents with distinct roles (e.g., Researcher retrieves and drafts, Critic checks the draft against retrieved sources for unsupported claims, Finalizer produces the polished answer).
- Expose at least one tool (e.g., the RAG retriever itself, or a document-lookup tool) as an MCP server, and have the agent call it via MCP rather than a direct function call.
- Implement a memory system: short-term (conversation buffer) and long-term (persisted user facts/preferences retrieved and injected into future sessions).

### Inputs
- The knowledge base from prior projects, plus at least one external tool/API (e.g., a live weather/stock API or a calculator) for the agent to choose between.
- 10 test queries spanning: "needs retrieval only," "needs a tool only," "needs both," and "needs multiple agents to collaborate."
- A returning-user scenario script (same simulated user across 2+ sessions) to test long-term memory.

### Expected Output
- A trace log (or visualized graph) for each test query showing the agent's tool-selection reasoning and the sequence of steps taken.
- A multi-agent transcript showing the Researcher/Critic/Finalizer (or equivalent) handoff, including at least one case where the Critic catches and corrects an unsupported claim.
- Confirmation that a tool call was routed through MCP (protocol-level evidence, e.g., request/response logs).
- A cross-session demo proving the agent recalls a fact/preference from an earlier session without it being restated by the user.

---

## Project 10 — "Ship It": Evaluation, Hallucination Detection, Guardrails & Load Testing
**Maps to modules:** `26.evaluation_with_ragasa`, `27.hallucination_detection`, `28.guardrails`, `29.loadtesting`

### Description
The capstone-of-the-capstone: harden the full system (from Projects 1–9) for production release.
Learners build an evaluation harness using RAGAS-style metrics, add automated hallucination
detection that flags ungrounded claims before they reach the user, wrap the system in guardrails
(input/output filtering for PII, prompt injection, off-topic/abusive queries, and unsafe outputs),
and run load tests to characterize the system's behavior and breaking point under concurrent
traffic.

### What the learner must do
- Build/curate an evaluation dataset (question, ground-truth answer, ground-truth source) of at least 30 examples covering the full knowledge base.
- Run RAGAS (or equivalent) metrics: faithfulness, answer relevance, context precision, context recall.
- Implement a hallucination detector: after generation, check whether each claim in the answer is supported by the retrieved context (e.g., via NLI/entailment check or LLM-as-judge), and flag/block unsupported answers.
- Add guardrails: input guardrail (block prompt injection attempts, off-topic/toxic queries, PII in queries) and output guardrail (block/redact PII in responses, refuse unsafe requests, enforce topic boundaries).
- Run a load test (e.g., Locust/k6) simulating increasing concurrent users against the Project 8 streaming API, and report throughput, error rate, and latency percentiles (p50/p95/p99) at each load level.

### Inputs
- The full system from Projects 1–9 (used as the system under test).
- A labeled evaluation dataset (30+ Q&A pairs with ground truth).
- A set of adversarial test inputs: prompt-injection attempts, off-topic/toxic queries, PII-containing queries, and questions designed to induce hallucination.
- A load-testing script/tool configured to ramp from 1 to N concurrent users.

### Expected Output
- A RAGAS evaluation report with faithfulness/relevance/precision/recall scores, including at least one round of pipeline improvement driven by these metrics (e.g., tune `k` or reranking after seeing low context precision) with before/after scores.
- A hallucination-detection log showing correctly flagged ungrounded answers, with a measured detection precision/recall on a labeled test set.
- A guardrail test report: pass/fail results against the adversarial input set (e.g., "9/10 prompt injection attempts blocked," "all PII in test queries redacted from logs/output").
- A load test report with a latency/error-rate graph across concurrency levels and a stated "safe operating capacity" (max concurrent users before SLA breach).
- A final one-page system architecture diagram showing how all 10 projects' components fit together into the shipped system.

---

## Suggested Flow Summary

| # | Project | Core Skill Unlocked |
|---|---------|---------------------|
| 1 | PDF Buddy | Chunking, embedding, vector DB, basic retrieval |
| 2 | Living Docs | Prompt engineering, document lifecycle management |
| 3 | No-Code RAG Ops | Workflow orchestration (n8n) |
| 4 | Smart Filter Search | Metadata filtering, reranking |
| 5 | Fast & Smart Query | Semantic caching, query expansion |
| 6 | Deep Retriever | Context compression, parent/multi-vector retrieval |
| 7 | Follow-Up Friendly | Multi-hop reasoning, conversational memory |
| 8 | RAG at Speed | Async pipelines, streaming APIs |
| 9 | Agent Team | Agentic/multi-agent RAG, MCP, long-term memory |
| 10 | Ship It | Evaluation, hallucination detection, guardrails, load testing |

Each project can be graded as a standalone deliverable, but the strongest capstone outcome is
having learners **carry one system forward** from Project 1 through Project 10, so the final
demo day is a single, fully evaluated, guardrailed, load-tested agentic RAG application.
