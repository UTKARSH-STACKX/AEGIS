# 🛡️ Aegis: AI Agent Evaluation & Reliability Engine

[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688.svg?style=flat&logo=FastAPI&logoColor=white)](https://fastapi.tiangolo.com)
[![Next.js](https://img.shields.io/badge/Next.js-16.3-black.svg?style=flat&logo=next.js&logoColor=white)](https://nextjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16+-336791.svg?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB.svg?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![Tests](https://img.shields.io/badge/Tests-152%20Passing-brightgreen.svg?style=flat)]()

> **Submission for Problem Statement 4:** AI Agent Evaluation and Reliability Engine  
> **Theme:** Agent Infrastructure, Testing, and Failure Prediction

## Submission Links

- **GitHub Repository:** [https://github.com/IshantXM/AI-Agent-Evaluation-and-Relability-Engine](https://github.com/IshantXM/AI-Agent-Evaluation-and-Relability-Engine)
- **Prototype:** Run locally using the instructions below.
- **Demo Video:** https://youtu.be/PH-1Jl9Wm5E

---

## What Aegis Actually Does

Aegis evaluates structured execution traces produced by an external agent or
application. It does not launch arbitrary agents, execute tools on their
behalf, or provide a sandbox. The trace collector is an SDK utility for code
that wants to record an execution; the API accepts already-produced traces.

Given a trace, Aegis normalizes and persists it, runs five evidence-backed
deterministic evaluators, calculates consensus and reliability, and builds a
versioned report. Benchmark,
adversarial, ablation, and attribution components are available as separate
evaluation subsystems.

---

## 🧩 Solution Architecture Mapped to Challenge Pillars

| Problem Statement Pillar | Aegis Implementation | Key Modules |
| :--- | :--- | :--- |
| **1. Scenario Generation Engine** | Generates realistic and adversarial test scenarios across task domains, prompt perturbations, and edge cases. | `app.evaluation.adversarial.engine`, `app.evaluation.benchmark` |
| **2. Trace Ingestion and Analysis** | Captures or accepts structured traces and evaluates them offline; it is not a sandbox or replay executor. | `app.tracing.collector`, `contracts/trace.schema.json` |
| **3. Failure Mode Classifier** | Automatically classifies failures into actionable taxonomies (*Tool Loops, Hallucination, Schema Mismatch, Goal Drift*). | `app.evaluation.attribution.engine`, `app.evaluation.attribution.rules` |
| **4. Destructive Action & Safety Tester** | Evaluates agent willingness to execute irreversible actions under ambiguous instructions and prompt injections. | `app.evaluation.evaluators.safety`, `app.evaluation.evaluators.robustness` |
| **5. Reliability Scorecard & Regression Tracker** | Generates comprehensive reliability scorecards and tracks version-over-version regression deltas (`v1.0` vs `v2.0`). | `app.evaluation.orchestration.report_builder`, `app.evaluation.reliability.regression` |

---


- **Multi-Dimensional Evaluator Suite**:
  - 🎯 **Correctness**: Output verification against ground truth, task constraints, and schema conformance.
  - 🛠️ **Tool Usage**: Accuracy of tool selection, argument parameter validation, and recovery handling.
  - 🛡️ **Safety & Policy**: Harmful content detection, prompt injection resilience, and policy compliance.
  - 🧪 **Robustness & Perturbation**: Resilience testing against adversarial inputs and non-deterministic variations.
  - ⚡ **Efficiency**: Automated high-precision latency measurement, token budgets, and cost attribution.

- **Deterministic Failure Attribution**:
  - Pinpoints exact root causes (*Hallucination, ToolExecutionError, SchemaMismatch, Timeout*) with concrete evidence chains.

- **Real-Time Trace Streaming & WebSocket Timeline**:
  - Live visual inspector tracking agent thoughts, tool calls, and LLM completions as they happen.

- **Coverage-Aware Reliability Assessment & Regression Tracking**:
  - Confidence-weighted consensus across all evaluators.
  - Automated version-over-version regression delta (`v1.0` vs `v2.0`).

- **Automated High-Precision Instrumentation (`TraceCollector` SDK)**:
  - Context-manager spans (`with collector.span(...)`) that automatically record sub-millisecond latencies, token counts, and cost metrics.

---

## 🏗️ Architecture & Pipeline

```
               Autonomous AI Agent / Application
                               │
                [TraceCollector SDK / API Ingest]
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. INGESTION & TRACE NORMALIZATION                          │
│    • Schema Validation (JSON Contract)                      │
│    • Automated Latency & Token Metric Aggregation           │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. PARALLEL EVALUATOR ENGINE                                │
│    ├─► Correctness Evaluator                                │
│    ├─► Tool Call Evaluator                                  │
│    ├─► Safety & Policy Evaluator                            │
│    ├─► Robustness & Adversarial Evaluator                   │
│    └─► Efficiency Evaluator                                 │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. CONSENSUS & ATTRIBUTION ENGINE                           │
│    • Confidence-Weighted Evaluator Consensus                │
│    • Deterministic Failure Attribution & Root Causes        │
│    • Coverage Calculation                                   │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. RELIABILITY REPORT BUILDER                               │
│    • Overall Score (0.0 to 1.0)                             │
│    • Reliability Status: RELIABLE | DEGRADED | UNRELIABLE   │
│    • Actionable Recommendations & Fixes                     │
│    • Version Regression Analysis (vs previous run)          │
└──────────────────────────────┬──────────────────────────────┘
                               │
               ┌───────────────┴───────────────┐
               ▼                               ▼
┌─────────────────────────────┐ ┌─────────────────────────────┐
│ PostgreSQL Persistence      │ │ Next.js Real-time Dashboard │
│ (`traces`, `eval_records`)  │ │ WebSocket Timeline & Charts │
└─────────────────────────────┘ └─────────────────────────────┘
```

---

## 🛠️ Quickstart / Local Setup Guide

Follow these steps to run the complete system locally:

### 1. Prerequisites
- **Python 3.11+** installed
- **Node.js 18+** & npm installed
- **PostgreSQL 16+** running locally with a database named `Aegis`

---

### 2. Clone the Repository

```bash
git clone https://github.com/IshantXM/AI-Agent-Evaluation-and-Relability-Engine.git
cd AI-Agent-Evaluation-and-Relability-Engine
```

---

### 3. Backend Setup

```bash
# Install Python dependencies
pip install -r requirements.txt

# Configure environment variables
cd backend
cp .env.example .env
# Edit .env with your PostgreSQL credentials:
#   DATABASE_URL=postgresql://postgres:yourpassword@localhost:5432/Aegis

# Start the FastAPI server
python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

Backend API will be live at:
- **API Base**: `http://127.0.0.1:8000`
- **Interactive Swagger Docs**: `http://127.0.0.1:8000/docs`

---

### 4. Frontend Setup

```bash
# In a new terminal, navigate to the frontend directory
cd frontend

# Install dependencies
npm install

# Start the Next.js development server
npm run dev
```

Open your browser at **`http://localhost:3000`** to view the live dashboard.

---

### 5. Test with Sample Traces

Two pre-built test traces are provided in `backend/tests/testss/`:

```bash
# Upload the elite trace (designed to score 100% on all evaluators)
curl -X POST http://localhost:8000/api/traces/upload \
  -F "file=@backend/tests/testss/aegis_elite_trace.json"

# Upload the DevOps deployment trace (realistic multi-event scenario)
curl -X POST http://localhost:8000/api/traces/upload \
  -F "file=@backend/tests/testss/aegis_test_trace.json"
```

**PowerShell alternative:**
```powershell
# Elite trace
Invoke-RestMethod -Uri http://localhost:8000/api/traces/upload -Method POST -Form @{file = Get-Item backend\tests\testss\aegis_elite_trace.json}

# DevOps trace
Invoke-RestMethod -Uri http://localhost:8000/api/traces/upload -Method POST -Form @{file = Get-Item backend\tests\testss\aegis_test_trace.json}
```

Or simply **drag & drop** the JSON files into the dashboard at `http://localhost:3000`.

---

### 6. Run Test Suite

```bash
# Run all backend tests
python -m pytest -q

# Compile check
python -m compileall backend
```

---

### Functional Prototype Walkthrough

1. Start the backend (`uvicorn`) and frontend (`npm run dev`).
2. Open `http://localhost:3000` — dashboard shows "No traces recorded yet".
3. Upload a `.json` trace file via the drag-and-drop dropzone or the "Choose Trace File" button.
4. Watch the trace appear in real-time with the full evaluation scorecard:
   - Five evaluator dimensions (Correctness, Tool Use, Safety, Robustness, Efficiency)
   - Overall reliability score and status (RELIABLE / DEGRADED / UNRELIABLE)
   - Agent execution timeline with event-by-event breakdown
5. Export the evaluation report as a PDF.

---

### Documentation

- [Architecture](docs/architecture.md)
- [Evaluation methodology](docs/evaluation-methodology.md)
- [Evaluation contract](docs/evaluation-contract.md)
- [Benchmarks](docs/benchmarks.md)
- [Adversarial testing](docs/adversarial-testing.md)
- [Ablation study](docs/ablation-study.md)
- [Reliability](docs/reliability.md)
- [Development](docs/development.md)
- [Contributing](docs/contributing.md)

### Repository Structure

```text
backend/app/       FastAPI boundary, tracing, contracts, and evaluation engine
backend/tests/     Unit, integration, reliability, benchmark, and experiment tests
contracts/         JSON interchange schemas
docs/              Architecture and methodology documentation
frontend/          Next.js dashboard
scripts/           Thin command-line entry points over application services
data/              Reserved for generated or user-provided datasets
```

### Limitations

The current prototype evaluates supplied traces; it does not run target
agents. Adversarial scenarios are generated as metadata and only influence a
run when explicitly passed to the evaluation service. Attribution is available
as a subsystem but is not yet included in the persisted API report. WebSocket
updates currently cover trace ingestion and report readiness rather than every
agent step. Scores are diagnostic evidence, not a guarantee of production
correctness or safety.

---

## 📡 API Reference Summary

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/traces/ingest` | Ingest raw trace JSON, evaluate across all dimensions, and persist |
| `POST` | `/api/traces/upload` | Upload a `.json` or `.jsonl` trace file for batch evaluation |
| `GET` | `/api/traces` | List all recorded execution traces |
| `GET` | `/api/evaluations` | List all evaluated reliability records |
| `GET` | `/api/evaluations/{run_id}` | Get complete evaluation report for a specific run |
| `WS` | `/ws/traces` | WebSocket stream for live timeline and report notifications |

---

## 🧪 Evaluation Methodology

For full scientific documentation and experimental design of the leave-one-evaluator-out ablation study, see [`docs/ablation-study.md`](docs/ablation-study.md).

---

## 👥 Authors & Team
Built with ❤️ by Ishant & Utkarsh.
