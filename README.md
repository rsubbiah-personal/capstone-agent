# Capstone Agent

A retrieval-augmented, policy-aware customer support agent with MCP tooling, safety
guardrails, RLHF feedback loops, monitoring, and an evaluation harness.

## Layout

| Path | Purpose |
| --- | --- |
| `agent/` | Core agent loop, prompts, memory, planner |
| `tool-retrieval/` | Document loading, chunking, embedding, FAISS store, retriever |
| `tools/` | Tool registry and individual tool implementations |
| `mcp/` | MCP server and client |
| `policy_rlhf/` | Policy checking, feedback collection, policy updates |
| `safety/` | Guardrails and PII filtering |
| `monitoring/` | LangSmith tracing and Langfuse logging |
| `evaluation/` | Test harness and metrics |
| `knowledge/` | Raw source documents, processed chunks, FAISS index |
| `data/` | Policy config, RLHF feedback store, evaluation rubric |
| `deployment/` | App config, runtime config, container definition |
| `scripts/` | Entry points for ingestion, indexing, running, and evaluation |
| `docs/` | Problem framing, demo script, evaluation and engineering write-ups |
| `logs/` | Runtime logs (gitignored) |

## Getting started

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env   # then fill in your keys
```

## Typical workflow

```bash
python scripts/ingest_documents.py     # load + chunk knowledge/raw -> knowledge/processed
python scripts/build_faiss_index.py    # embed chunks -> knowledge/faiss_index
python scripts/start_mcp_server.py     # run the MCP server
python scripts/run_agent.py            # interact with the agent
python scripts/run_evaluation.py       # score the agent against the rubric
python scripts/run_rlhf_pipeline.py    # fold collected feedback into policy
```
