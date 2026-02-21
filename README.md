# AI Study Planner

> LLM-powered study planning system that converts unstructured course syllabi into structured weekly study plans using LangChain + schema-validated outputs.

## Project Goal

**Main objective**

Build an AI-driven study planner that:

- Parses raw syllabus text into structured data
- Generates realistic weekly study plans based on constraints
- Supports plan revision when conditions change
- Ensures reliability via schema validation and deterministic scheduling logic

**Why this project exists**

Traditional LLM apps often generate unreliable outputs.  
This project focuses on:

- Structured AI outputs
- Data validation
- Hybrid AI + deterministic logic

## Project Scope

### Included (MVP)
- Syllabus → structured topics extraction (LLM)
- Weekly plan generation (heuristic scheduling)
- Plan revision via natural language requests
- Streamlit UI
- Save/load plans
- JSON/CSV export

## Core AI/Data Concepts

This project focuses on:

- **Structured LLM Outputs**
  - Pydantic schema validation
- **Hybrid Systems**
  - LLM for parsing + reasoning
  - Deterministic algorithm for scheduling
- **Robustness**
  - JSON repair fallback
  - Validation before execution
- **Data Modeling**
  - Topics, assessments, tasks, weekly plans

## Architecture Overview

```
User Input (Syllabus + Constraints)
        ↓
LLM Parser (LangChain)
        ↓
Validated Structured Data (Pydantic)
        ↓
Deterministic Planner (Python logic)
        ↓
Weekly Study Plan
        ↓
Revision Agent (LLM + validation)
        ↓
Updated Plan
```

## Project Structure

```
study-planner/
│
├── app.py                 # Streamlit entry point
│
├── core/
│   ├── schemas.py         # Pydantic data models
│   ├── parser.py          # Syllabus → structured data
│   ├── planner.py         # Scheduling heuristic
│   ├── reviser.py         # Plan revision logic
│   ├── storage.py         # Save/load plans
│   └── utils.py
│
├── data/                  # Saved plans
├── requirements.txt
└── README.md
```

## Data Model (High Level)

### Topic
- name
- difficulty (1–5)
- estimated_hours
- prerequisites (optional)

### Assessment
- type (midterm/final/etc.)
- date
- weight

### Task
- title
- hours
- category (reading/practice/review)
- related topic

### CoursePlan
- weeks[]
- risk_flags
- assumptions

## Workflow

### 1) Parsing Stage
Input:
- Raw syllabus text

Output:
- Structured topics + assessments

Key idea:
- LLM generates JSON
- JSON validated with Pydantic

### 2) Planning Stage
Input:
- Parsed syllabus
- User constraints (hours/week)

Process:
- Priority scoring
- Week allocation
- Exam buffers

Output:
- Deterministic weekly plan

### 3) Revision Stage
User can request:

- “I missed 4 hours”
- “Midterm moved earlier”
- “More practice, less reading”

LLM updates plan → validated again.

## Example Use Case

1. User pastes syllabus text
2. AI extracts topics and assessments
3. Planner generates weekly schedule
4. User revises plan after missing study time
5. Updated schedule is generated automatically

## Evaluation / Metrics

Tracked metrics:

- Parsing latency
- Planning latency
- Revision latency
- (Optional) token usage

## Tech Stack

- Python
- LangChain
- Pydantic
- Streamlit
- SQLite / JSON storage

## Development Plan (3 Weeks)

### Week 1 — AI/Data Foundation
- Define schemas
- Build syllabus parser
- Implement planner heuristic

### Week 2 — MVP Product
- Streamlit UI
- Storage
- Export functionality

### Week 3 — Revision + Polish
- Revision pipeline
- UX improvements
- Deployment + documentation

## Design Decisions

### Why deterministic planning?
LLMs are great for interpretation but weak at consistent scheduling logic.

### Why schema validation?
Prevents malformed AI outputs and increases reliability.

## Limitations

- Single-course planning only
- No calendar sync
- Heuristic scheduling (not optimization-based)
- Depends on syllabus quality

## Future Improvements

- Multi-course optimization
- Calendar integration (.ics)
- Adaptive workload estimation
- RAG over lecture notes
- Difficulty estimation via historical data

## Running Locally

```bash
git clone <repo-url>
cd study-planner
pip install -r requirements.txt
streamlit run app.py
```
