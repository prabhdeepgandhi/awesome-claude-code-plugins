---
description: Launches backend and frontend agents in parallel worktrees. Use after /kickoff has generated plan.md and scaffold.
argument-hint: Optional instructions (e.g. "focus on the dashboard page first")
---

# Parallel Build

You are a build coordinator for a 30-minute interview POC. Launch two parallel subagents that build backend and frontend simultaneously, then integrate locally.

## Prerequisites Check

1. Read `plan.md` — extract backend tasks and frontend tasks
2. Read `SYSTEM-DESIGN.md` — extract API contract
3. Verify scaffold exists: `backend/app/main.py` and `frontend/src/App.tsx`

If any missing, tell user to run `/kickoff` first.

Additional instructions: $ARGUMENTS

## Step 1: Create API Contract

Create `API-CONTRACT.md` from SYSTEM-DESIGN.md endpoints — shared contract both agents follow.

## Step 2: Launch Both Agents in Parallel

IMPORTANT: Launch Steps 2a and 2b at the SAME TIME using two parallel Agent tool calls. Do NOT wait for one to finish before starting the other.

### Step 2a: Backend Agent

Use the Agent tool to spawn a subagent with this prompt:

```
You are building the backend for an interview POC. Read API-CONTRACT.md and plan.md for context.

Work in the backend/ directory. Build:
- SQLAlchemy models from data model in SYSTEM-DESIGN.md
- Pydantic request/response schemas matching API-CONTRACT.md
- FastAPI route handlers for all endpoints
- Database initialization (SQLite for MVP)
- Add CORS middleware allowing localhost:3000
- Test each endpoint with curl commands

When done, verify the server starts: cd backend && uvicorn app.main:app --reload --port 8000
```

### Step 2b: Frontend Agent

Use the Agent tool to spawn a subagent with this prompt:

```
You are building the frontend for an interview POC. Read API-CONTRACT.md and plan.md for context.

Work in the frontend/ directory. Build:
- TypeScript types/interfaces matching API-CONTRACT.md schemas
- React components for each page/view
- API client functions using axios pointing to http://localhost:8000
- Basic routing with react-router-dom
- Tailwind styling for clean presentation

When done, verify the dev server starts: cd frontend && npm run dev -- --port 3000
```

## Step 3: Local Integration

After BOTH agents complete:
1. Start backend: `cd backend && uvicorn app.main:app --reload --port 8000`
2. Start frontend: `cd frontend && npm run dev -- --port 3000`
3. Test end-to-end flow between the two local servers
4. Fix any integration issues (CORS, URL mismatches, type mismatches)

Skip Docker for MVP. Use `/docker-integrate` after MVP verified working locally.

## Step 4: Final Commit

```bash
git add -A
git commit -m "feat: complete MVP implementation"
```
