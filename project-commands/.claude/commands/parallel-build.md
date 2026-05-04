---
description: Launches backend and frontend agents in parallel worktrees. Use after /kickoff has generated plan.md and scaffold.
argument-hint: Optional instructions (e.g. "focus on the dashboard page first")
---

# Parallel Build

You are a build coordinator for a 30-minute interview POC. Launch two parallel agents that build backend and frontend simultaneously, then integrate.

## Prerequisites Check

1. Read `plan.md` — extract backend tasks and frontend tasks
2. Read `SYSTEM-DESIGN.md` — extract API contract
3. Verify scaffold exists: `backend/app/main.py` and `frontend/src/App.tsx`

If any missing, tell user to run `/kickoff` first.

Additional instructions: $ARGUMENTS

## Step 1: Create API Contract

Create `API-CONTRACT.md` from SYSTEM-DESIGN.md endpoints — shared contract both agents follow.

## Step 2: Launch Backend Agent

Spawn an agent with isolation: worktree to build:
- SQLAlchemy models from data model
- Pydantic request/response schemas
- FastAPI route handlers for all endpoints
- Database initialization
- Test with `curl` commands

## Step 3: Launch Frontend Agent

Spawn an agent with isolation: worktree to build:
- TypeScript types matching API schemas
- React components for each page/view
- API client functions using axios
- Basic routing with react-router-dom
- Tailwind styling

## Step 4: Integration

After both agents complete:
1. Merge both worktrees
2. Verify `docker-compose up` works
3. Test end-to-end flow
4. Fix any integration issues (CORS, URL mismatches, type mismatches)

## Step 5: Final Commit

```bash
git add -A
git commit -m "feat: complete MVP implementation"
```
