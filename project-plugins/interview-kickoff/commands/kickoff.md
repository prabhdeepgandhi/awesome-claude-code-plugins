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

Create a system design document. Think like a senior architect in an interview.

Output a `SYSTEM-DESIGN.md` file with:

### 2.1 Architecture Overview
- Draw ASCII diagram showing: Client (React) → API Gateway → FastAPI Backend → Database
- Include any additional services (cache, queue, etc.) only if truly needed

### 2.2 Data Model
- List entities with fields and types
- Show relationships (1:1, 1:N, N:N)
- Keep it minimal — only what MVP needs

### 2.3 API Endpoints
- List all REST endpoints: method, path, request/response
- Group by resource
- Include auth endpoints if needed

### 2.4 Tech Stack Decision
- Backend: Python FastAPI + SQLAlchemy + SQLite (MVP) or PostgreSQL
- Frontend: React + TypeScript + Vite + Tailwind CSS
- Infrastructure: Docker + docker-compose
- State why each choice fits the 30-min constraint

## Phase 3: Plan Document (2 min)

Create `plan.md` with:

### 3.1 MVP Scope (RICE Prioritized)
Rate each feature using simplified RICE:
- **R**each: How many users need this? (1-3)
- **I**mpact: How critical to demo? (1-3)
- **C**onfidence: Can we build in time? (1-3)
- **E**ffort: Minutes to implement (estimate)

Score = (R × I × C) / E — sort descending, draw the cutoff line at 25 min total effort.

### 3.2 Build Order (Parallelizable)
Split into:
- **Backend tasks** (can run in parallel chat)
- **Frontend tasks** (can run in parallel chat)
- **Integration tasks** (must be sequential after both)
- **Docker tasks** (can run in parallel)

### 3.3 File Structure
```
project-root/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   ├── routes/
│   │   └── database.py
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── App.tsx
│   │   ├── components/
│   │   ├── pages/
│   │   ├── api/
│   │   └── types/
│   ├── package.json
│   └── Dockerfile
├── docker-compose.yml
├── plan.md
├── SYSTEM-DESIGN.md
├── CLAUDE.md
└── README.md
```

### 3.4 Time Budget
```
0-5 min:   This kickoff (design + plan)
5-10 min:  Project scaffold + Docker setup
10-20 min: Backend API + Frontend UI (PARALLEL)
20-25 min: Integration + wiring
25-28 min: Demo polish + final commits
28-30 min: Double-check + push to GitHub
```

## Phase 4: Scaffold (3 min)

Generate the actual project files:

### 4.1 Backend Scaffold
- `backend/app/main.py` — FastAPI app with CORS, health check
- `backend/app/database.py` — SQLAlchemy setup with SQLite
- `backend/app/models.py` — SQLAlchemy models from data model
- `backend/app/schemas.py` — Pydantic schemas
- `backend/requirements.txt` — fastapi, uvicorn, sqlalchemy, pydantic
- `backend/Dockerfile` — Python slim, multi-stage not needed for MVP

### 4.2 Frontend Scaffold
Run: `npm create vite@latest frontend -- --template react-ts`
- `frontend/src/api/client.ts` — axios instance pointing to backend
- `frontend/src/types/index.ts` — TypeScript types matching schemas
- `frontend/tailwind.config.js` — if using Tailwind

### 4.3 Docker Scaffold
- `docker-compose.yml` — backend + frontend + db (if PostgreSQL)
- `backend/Dockerfile`
- `frontend/Dockerfile`

### 4.4 Project Meta
- `CLAUDE.md` — project context for Claude Code
- `README.md` — one-paragraph description + how to run
- `.gitignore` — Python + Node + Docker ignores

## Phase 5: Git Init + First Commit

```bash
git init
git add -A
git commit -m "feat: initial project scaffold with FastAPI + React + Docker"
```

If GitHub repo URL provided, also:
```bash
git remote add origin <url>
git push -u origin main
```

## RULES
- Do NOT ask more than 5 questions total
- Do NOT add features beyond MVP scope
- Do NOT set up testing frameworks (no time)
- Do NOT add authentication unless explicitly requested
- Do NOT use ORMs beyond basic SQLAlchemy
- SQLite is fine for MVP — don't set up PostgreSQL unless docker-compose makes it trivial
- Every file should be functional, not a placeholder
- Prefer inline styles or basic Tailwind over complex CSS setups
