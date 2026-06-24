# Applied AI — Self-Study Learning Path

A personal learning path derived from **Arpit Bhayani's Applied AI Masterclass** curriculum
(https://arpitbhayani.me/applied-ai), structured for self-study using **opencode + GLM-5.2**
as your instructor and **free-tier LLM APIs** for prototyping.

> Course stats: 6 sessions · 7 systems · 3 weeks (live cohort cadence).
> Prototype count on the portal is **inconsistent**: banner says 26, "Key Details" says 24,
> and the per-session counts sum to 27 (6+7+6+3+3+2). Treat the exact total as ambiguous.
> This plan adds a Phase 0 ramp-up, so expect **~4–5 weeks** at 10+ hrs/week.
>
> Scope: the course **does not cover Machine Learning or Deep Learning** — the focus is on
> leveraging LLMs, understanding patterns/pitfalls, and building reliable systems with them.

---

## How to use this file

- Every learning item is a checkbox: `- [ ]` = not done, `- [x]` = done.
- In any GitHub-flavored Markdown renderer (VS Code preview, Obsidian, GitHub, etc.) you can
  click checkboxes to toggle them. In a plain editor, just edit `- [ ]` ↔ `- [x]`.
- Work top to bottom. Phases are sequential — each builds on the previous.
- The **Progress** table at the bottom auto-summarizes where you are (update counts as you go).

### How to use opencode/GLM-5.2 as your instructor

- **Explain**: "Explain ReAct loop from first principles with a minimal Python example."
- **Prototype**: "Write a minimal prototype for semantic caching using Gemini API."
- **Review**: paste your code and ask "What are the failure modes and edge cases here?"
- **Brainstorm systems**: "Design a fact-checking agentic system. What are the components,
  failure modes, and evaluation strategy?"
- **Debug**: paste errors/stack traces directly.
- Do **not** treat me as the LLM inside your Python prototypes — use a real API endpoint
  (see Tooling below) for programmatic calls. I'm your tutor/code-reviewer, not the runtime.

---

## Critical: Tooling & API setup (free tier, no paid API)

The course requires your own API keys for prototyping. You have opencode/GLM-5.2 (tutor) +
Gemini UI (free web), but **no paid API**. Use a free-tier programmatic API for the LLM calls
*inside* your prototypes. Recommended, in priority order:

- [ ] **Google AI Studio — Gemini API free tier** (PRIMARY). Aligns with the course's Gemini
      examples; you already have a Google account via Gemini UI. Get a key at
      https://aistudio.google.com. **Verify current free-tier rate limits yourself** (RPM,
      tokens/day) — they change over time and vary by model (Flash vs Pro).
- [ ] **Groq free tier** — very fast, generous free limits, good for prototyping loops.
      https://console.groq.com
- [ ] **OpenRouter free models** — access several models with free quota.
      https://openrouter.ai
- [ ] **Ollama (local)** — run models on your machine, fully free/offline, needs decent hardware.
      https://ollama.com
- [ ] Pick **one** primary provider now and store the key in a `.env` (never commit it).
- [ ] Install Python deps for the course: `httpx` or `requests`, `pydantic`, the provider SDK
      (e.g. `google-generativeai`), `python-dotenv`, `pytest`, `rich` (nice logs).

> Note: The course's official prototypes may use Gemini-specific features. With free-tier
> Gemini you can follow most examples directly; on other providers you'll translate the call
> shape. Ask me to port any example.

---

## Table of Contents

- [Phase 0 — Fundamentals / Ramp-up](#phase-0--fundamentals--ramp-up)
- [Phase 1 — Prompt LLMs Reliably (W1S1)](#phase-1--prompt-llms-reliably-w1s1)
- [Phase 2 — Tool Use and RAG in Production (W1S2)](#phase-2--tool-use-and-rag-in-production-w1s2)
- [Phase 3 — Building Agents That Work (W2S1)](#phase-3--building-agents-that-work-w2s1)
- [Phase 4 — Multi-Agent Systems and Memory (W2S2)](#phase-4--multi-agent-systems-and-memory-w2s2)
- [Phase 5 — Evaluation, Safety, and Agentic Systems (W3S1)](#phase-5--evaluation-safety-and-agentic-systems-w3s1)
- [Phase 6 — Production Architecture and Scale (W3S2)](#phase-6--production-architecture-and-scale-w3s2)
- [Free supplementary viewing](#free-supplementary-viewing)
- [Progress](#progress)

---

## Phase 0 — Fundamentals / Ramp-up

> Goal: satisfy the course prerequisites so Week 1 lands cleanly. ~1 week at 10+ hrs.
> Pre-reqs per portal: basic Python, basic system design, official Pre-reads, API access.

### 0.1 Python essentials for AI prototyping

- [ ] Virtual environments & packaging (`venv`, `pip`, `requirements.txt`, `.env` loading)
- [ ] HTTP calls with `httpx`/`requests` (sync + async), handling timeouts & status codes
- [ ] JSON handling, nested data, error-tolerant parsing
- [ ] `pydantic` for typed/structured data and validation (foundation for structured outputs)
- [ ] Basic OOP: classes, composition, small interfaces (foundation for agent/tool abstractions)
- [ ] `async`/`await` basics and concurrency (needed for parallel tool calls later)
- [ ] Logging with `rich` or `logging` (you'll need observability from day one)

### 0.2 Basic system design refresh

- [ ] API design: idempotency, retries with exponential backoff + jitter
- [ ] Caching fundamentals: cache keys, TTL, invalidation, hit/miss
- [ ] Rate limiting & quotas (matters a lot with free-tier LLM APIs)
- [ ] Queues / async job handoff basics
- [ ] Observability: structured logs, metrics, tracing mental model
- [ ] Failure handling: timeouts, partial failures, graceful degradation

### 0.3 Official Pre-reads

- [ ] Read and understand the course Pre-reads doc:
      https://docs.google.com/document/d/1hBdMSxfCwD0XQVMXVM0y_Kvk5YlG6hO-w3yDOJTiu3I/edit?tab=t.0
- [ ] Note any terms/concepts you don't fully grasp → ask me to explain each

### 0.4 First call checkpoint

- [ ] Make one successful programmatic LLM call from Python using your chosen free-tier API
- [ ] Wrap it in a tiny function with timeout + retry + error handling
- [ ] Commit this as your `prototype-00` starter

---

## Phase 1 — Prompt LLMs Reliably (W1S1)

> Foundation session. Establishes dependable AI apps. Portal lists **6 prototypes** +
> system: **Fact Checking Agentic System**.

### Concepts to study

- [ ] Stochastic LLMs — why outputs vary, temperature/sampling, determinism strategies
- [ ] Chain-of-Thought (CoT) Prompting
- [ ] Few-shot Prompting
- [ ] Prompt Failure Modes — common ways prompts break
- [ ] Structured Outputs — JSON/schema enforcement (tie to `pydantic`)
- [ ] Prompting Reliably — patterns for consistent, dependable outputs

### Prototypes to build (6 — suggested directions)

> The portal does NOT name the official prototypes. These 6 are **my suggestions** derived
> from the session's concepts; replace any with your own.

- [ ] P1.1 — Same prompt, vary temperature/top-p; measure output variance
- [ ] P1.2 — CoT vs direct prompting on a reasoning task; compare correctness
- [ ] P1.3 — Few-shot prompt builder with a reusable example template
- [ ] P1.4 — Reproduce a prompt failure mode (e.g. ambiguous instruction) and fix it
- [ ] P1.5 — Structured output enforcer: force JSON matching a `pydantic` schema
- [ ] P1.6 — A "prompting reliably" wrapper: retries + validation + fallback on bad output

### System design brainstorm

- [ ] **Fact Checking Agentic System** — sketch architecture: claim extraction, evidence
      retrieval, verification, confidence scoring. Identify failure modes + eval approach.

---

## Phase 2 — Tool Use and RAG in Production (W1S2)

> Production tool use + robust RAG. Portal lists **7 prototypes** +
> system: **RAG over 10M docs, no Hallucinations**.

### Concepts to study

- [ ] Tool Use and Tool Schema Design
- [ ] Parallel Tool Calls and Partial Failures
- [ ] Hybrid Search and Metadata Filtering
- [ ] Re-ranking — Cross Encoders and Bi-encoders
- [ ] Query Rewriting
- [ ] Semantic Caching

### Prototypes to build (7 — suggested directions)

> Portal does NOT name official prototypes. These are **my suggestions** from the concepts.

- [ ] P2.1 — Define a tool schema (JSON) and have the LLM call it correctly
- [ ] P2.2 — Multiple tools in parallel; handle one tool failing while others succeed
- [ ] P2.3 — Hybrid search: combine keyword (BM25) + vector search over a small corpus
- [ ] P2.4 — Metadata filtering on a vector store (source/date/type filters)
- [ ] P2.5 — Re-rank retrieved chunks with a cross-encoder; measure precision lift
- [ ] P2.6 — Query rewriting: expand/reformulate user query before retrieval
- [ ] P2.7 — Semantic cache: return cached answer for semantically-similar repeated queries

### System design brainstorm

- [ ] **RAG over 10M docs, no Hallucinations** — indexing/sharding strategy, retrieval pipeline,
      grounding/citation enforcement, hallucination prevention, scale & cost tradeoffs.

---

## Phase 3 — Building Agents That Work (W2S1)

> Core agent patterns: reason, plan, act beyond single calls. Portal lists **6 prototypes** +
> system: **Paper to Code Agent**.

### Concepts to study

- [ ] Observe-Think-Act Loop
- [ ] Ralph Loop
- [ ] ReAct Loop
- [ ] Plan and Execute Loop
- [ ] File System as Context
- [ ] Checkpoint and Resume
- [ ] Human in the Loop

### Prototypes to build (6 — suggested directions)

> Portal does NOT name official prototypes. These are **my suggestions** from the concepts.

- [ ] P3.1 — Observe-Think-Act loop on a simple task (e.g. inspect → reason → act)
- [ ] P3.2 — ReAct loop agent with 2–3 tools; trace its thought/action sequence
- [ ] P3.3 — Plan-and-Execute: planner generates steps, executor runs them
- [ ] P3.4 — File-system-as-context agent that reads/writes files to maintain state
- [ ] P3.5 — Checkpoint & resume: save agent state, kill process, resume from checkpoint
- [ ] P3.6 — Human-in-the-loop gate: pause for approval before a destructive action

### System design brainstorm

- [ ] **Paper to Code Agent** — parse a paper/spec → plan modules → generate code → test →
      iterate. Design loops, checkpoints, eval of generated code, failure recovery.

---

## Phase 4 — Multi-Agent Systems and Memory (W2S2)

> Multi-agent collaboration + memory. Portal lists **3 prototypes** +
> system: **Incident Auto-remediation System**.

### Concepts to study

- [ ] Memory Architecture
- [ ] Working Memory Management and Budgeting
- [ ] Memory Summarization and Write Strategies
- [ ] Orchestrator + Specialist Pattern
- [ ] Critic + Refiner Pattern
- [ ] Mixture of Agents Pattern
- [ ] Deadlocks in Multi-agent Systems

### Prototypes to build (3 — suggested directions)

> Portal does NOT name official prototypes. These are **my suggestions** from the concepts.

- [ ] P4.1 — Memory store with working-memory budget: trim/summarize when context grows
- [ ] P4.2 — Orchestrator + 2 specialists (e.g. researcher + writer) coordinated by an orchestrator
- [ ] P4.3 — Critic + Refiner loop on an output; detect and break a simulated deadlock

### System design brainstorm

- [ ] **Incident Auto-remediation System** — detect → diagnose → remediate agents, memory of
      past incidents, human escalation, safety guardrails, observability.

---

## Phase 5 — Evaluation, Safety, and Agentic Systems (W3S1)

> Systematic eval + trust. Portal lists **3 prototypes** + **2 systems**:
> **AI Code Reviewer System** and **Self-Updating AI Documentation Platform**.

### Concepts to study

- [ ] What makes a good eval?
- [ ] LLM-as-Judge
- [ ] Placing and Plugging Evals
- [ ] Human Evals
- [ ] Exploratory and Adversarial Evals
- [ ] Regression Harness

### Prototypes to build (3 — suggested directions)

> Portal does NOT name official prototypes. These are **my suggestions** from the concepts.

- [ ] P5.1 — LLM-as-judge eval on a set of outputs; compare against your own rubric
- [ ] P5.2 — Adversarial eval set: craft inputs that should break the system; measure failures
- [ ] P5.3 — Regression harness: run a frozen eval suite on every change to your prompt/agent

### System design brainstorms (2)

- [ ] **AI Code Reviewer System** — review pipeline, eval of review quality, false-positive
      handling, integration into dev workflow, safety on auto-suggestions.
- [ ] **Self-Updating AI Documentation Platform** — detect doc drift, propose updates, verify
      accuracy, versioning, eval loop, human approval gate.

---

## Phase 6 — Production Architecture and Scale (W3S2)

> Scalable, reliable, observable AI in production. Portal lists **2 prototypes** +
> system: **Natural Language Workflow Engine**.

### Concepts to study

- [ ] Graceful Degradation
- [ ] Prompt Caching
- [ ] Observability and Cost Attribution
- [ ] Brainstorming Production Gotchas

### Prototypes to build (2 — suggested directions)

> Portal does NOT name official prototypes. These are **my suggestions** from the concepts.

- [ ] P6.1 — Graceful degradation: fallback chain when the primary LLM/tool fails or times out
- [ ] P6.2 — Cost + latency observability: attribute tokens/$/ms per request and per agent step

### System design brainstorm

- [ ] **Natural Language Workflow Engine** — NL → workflow DAG, reliability, replayability,
      cost controls, observability, degradation strategy, multi-tenant concerns.

---

## Capstone

> The FAQ states: *"I would recommend you implement the core of every single system we
> discuss."* Aim to implement the core of all 7 systems; pick one as your deep capstone.

- [ ] Implement the **core** of each of the 7 systems (lightweight versions are fine)
- [ ] Pick **one** system and build it out end-to-end as your deep capstone
- [ ] Add an eval suite + regression harness from Phase 5 to your capstone
- [ ] Write a short post-mortem: what failed, what you'd harden for production

---

## Free supplementary viewing

> Free Arpit Bhayani videos linked on the portal under "Teaching style" — watch anytime to
> get a feel for the depth and teaching approach before/during the plan.

- [ ] https://youtu.be/wXvljefXyEo
- [ ] https://youtu.be/9iAJjtvBwyI
- [ ] https://youtu.be/3G293is403I
- [ ] https://youtu.be/roNgG4QVjTU
- [ ] https://youtu.be/LXhgFAZroG8
- [ ] https://youtu.be/FtJPvgMsn-Q

---

## Progress

Update counts as you check items off. (X / total per phase.)

| Phase | Topic | Concepts | Prototypes | Systems | Status |
|-------|-------|----------|------------|---------|--------|
| 0 | Fundamentals / Ramp-up | 0/19 | 0/1 | — | not started |
| 1 | Prompt LLMs Reliably | 0/6 | 0/6 | 0/1 | not started |
| 2 | Tool Use and RAG | 0/6 | 0/7 | 0/1 | not started |
| 3 | Building Agents | 0/7 | 0/6 | 0/1 | not started |
| 4 | Multi-Agent & Memory | 0/7 | 0/3 | 0/1 | not started |
| 5 | Evaluation & Safety | 0/6 | 0/3 | 0/2 | not started |
| 6 | Production & Scale | 0/4 | 0/2 | 0/1 | not started |
| — | Capstone | — | — | 0/10 | not started |

**Totals:** 0/55 concepts · 0/28 prototypes · 0/10 system tasks
(prototype count is my suggested allocation; the course cites 26 prototypes total — adjust as you go.)

---

## Source & attribution

- Curriculum source: https://arpitbhayani.me/applied-ai (Arpit Bhayani, Applied AI Masterclass)
- Official Pre-reads: https://docs.google.com/document/d/1hBdMSxfCwD0XQVMXVM0y_Kvk5YlG6hO-w3yDOJTiu3I/edit?tab=t.0
- This is a self-study plan derived from the public curriculum outline. The named systems are
  from the portal; the prototype suggestions are mine and are NOT the course's official
  prototypes. Verify everything independently.
