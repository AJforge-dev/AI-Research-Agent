# AI Research Agent — Autonomous Evidence-Based Research & Report Generation System

**Author:** Ajaykumar J
**Type:** AI Engineering Portfolio Project (in progress)

## Problem
Most "AI research agents" are just `LLM + search API + summary`, with no way to verify
whether generated claims are actually supported by the sources they cite. This project
builds a system that grounds every claim in traceable evidence, flags conflicting
sources, and reports uncertainty instead of hiding it.

## Core Idea
Structured pipeline: **Claim → Evidence → Source → Verification**, instead of blind
LLM summarization. For key claims, the system tracks:
```
{
  "claim": "...",
  "evidence": "...",
  "source": "...",
  "publication_date": "...",
  "confidence": 0.0,
  "supports_claim": true
}
```

## Target Architecture
```
User → Planner → Query Generator → Search Tools → Source Collection
→ Source Quality Evaluation → Document Processing → Document Store
→ RAG / Vector Retrieval → Evidence Extraction → Claim Extraction
→ Claim–Evidence Matching → Claim Verification → Conflict Detection
→ Evidence Quality Evaluation → Research Sufficiency Check
→ (Additional Search if needed) → Report Generation
→ Citation Generation → Evaluation → Final Research Report
```

## Tech Stack
- **Language:** Python
- **LLM:** OpenAI API (local models via Ollama explored later)
- **Agent framework:** Manual tool-calling first → LangGraph
- **RAG:** ChromaDB (PostgreSQL + pgvector if justified later)
- **Backend:** FastAPI
- **Frontend:** Streamlit
- **Database:** SQLite (Postgres later if justified)
- **Deployment:** Docker, GitHub

## Development Phases
| Level | Phase | Description |
|---|---|---|
| 1 | Basic LLM Researcher | Question → search queries → web search → summary |
| 2 | Tool-Using Researcher | Explicit tool calling (search_web, open_url, extract_content) |
| 3 | RAG Researcher | Chunking, embeddings, ChromaDB retrieval |
| 4 | Stateful Agent | LangGraph nodes: Planner, Researcher, Evidence Extractor, Fact Checker, Report Writer |
| 5 | Evidence Verification | Structured claim/evidence model, source quality, confidence scoring |
| 6 | Conflict-Aware Research | Detects and explains disagreeing sources instead of silently picking one |
| 7 | Persistent Research Memory | SQLite-backed sessions, follow-up question support |
| 8 | Evaluated Research System | Retrieval precision/recall, citation correctness, faithfulness, cost, latency |
| 9 | Production API/UI | FastAPI + Streamlit, logging, error handling, Docker |
| 10 | Cloud vs Local Model Eval | Ollama on Apple Silicon vs OpenAI API, compared on quality/latency/cost |

## Key Engineering Features
- Explicit conflict detection between disagreeing sources (with likely explanations:
  different reporting periods, currencies, estimates vs actuals, etc.)
- Source quality tiering (government/primary research > journalism/industry reports > blogs/forums)
- Research sufficiency checks with bounded iteration (no infinite research loops)
- Full observability: structured logs of every agent action (search, retrieval, conflict, report)
- Cost tracking: LLM calls, tokens, search calls, estimated $ per research session
- Prompt-injection–aware design: retrieved webpage content always treated as untrusted data, never as instructions

## Evaluation Plan
Baseline (LLM-only) → RAG → Agent → Agent + Verification, measured on:
retrieval precision/recall, citation correctness, faithfulness, completeness,
latency, API cost, failure rate. No fabricated metrics — only measured results.

## Current Status
Phase 0 (environment setup, repo initialized) complete. Actively building Phase 1
(basic LLM researcher pipeline).

## Author Background
B.Tech, Artificial Intelligence & Data Science, GTEC, Vellore, Tamil Nadu (2027).
IoT Developer, Myme Techies. Founder, Ashvex (Software/AI/Drone divisions).
