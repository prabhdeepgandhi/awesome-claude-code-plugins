---
description: Kickoff an interview POC project in under 30 minutes. Generates system design, plan.md, and full project scaffold with FastAPI + React + Docker.
argument-hint: Describe the system you want to build (e.g. "URL shortener with analytics dashboard")
---

# Interview Kickoff

You are orchestrating a 30-minute interview POC build. Speed is critical. No over-engineering. MVP only.

**Project idea:** $ARGUMENTS

## Phase 1: Quick Requirements (2 min)

Ask the user UP TO 3 focused questions to clarify:
1. Core user flow (what does the user DO?)
2. Key data entities (what are we storing?)
3. Must-have vs nice-to-have features

If the description is already clear enough, skip questions and state your assumptions.

## Phase 2: System Design (3 min)

Create `SYSTEM-DESIGN.md` with:
- ASCII architecture diagram (Client → API → Backend → DB)
- Data model with entities, fields, relationships
- API endpoints grouped by resource
- Tech stack: FastAPI + SQLAlchemy + SQLite, React + TypeScript + Vite + Tailwind, Docker

## Phase 3: Plan Document (2 min)

Create `plan.md` with:
- MVP scope using RICE prioritization
- Build order (backend tasks, frontend tasks, integration tasks)
- File structure
- Time budget (5 min kickoff, 5 min scaffold, 10 min parallel build, 5 min integration, 3 min polish)

## Phase 4: Scaffold (3 min)

Generate project files:
- `backend/app/main.py` — FastAPI app with CORS, health check
- `backend/app/database.py` — SQLAlchemy + SQLite
- `backend/app/models.py` — SQLAlchemy models
- `backend/app/schemas.py` — Pydantic schemas
- `backend/requirements.txt`
- `backend/Dockerfile`
- `frontend/` — Vite React TypeScript app
- `frontend/src/api/client.ts` — axios instance
- `frontend/src/types/index.ts`
- `docker-compose.yml`
- `CLAUDE.md`, `README.md`, `.gitignore`

## Phase 5: Git Init

```bash
git init
git add -A
git commit -m "feat: initial project scaffold with FastAPI + React + Docker"
```

## RULES
- Do NOT ask more than 3 questions
- Do NOT add features beyond MVP
- Do NOT set up testing frameworks
- Do NOT add auth unless requested
- SQLite for MVP
- Every file must be functional, not a placeholder
