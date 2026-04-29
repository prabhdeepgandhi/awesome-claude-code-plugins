---
description: Launches backend and frontend agents in parallel. Each works in isolated worktree. Use after /interview-kickoff has generated plan.md and project scaffold.
argument-hint: Optional specific instructions (e.g. "focus on the dashboard page first")
---

# Parallel Build

You are a build coordinator for a 30-minute interview POC. Your job is to launch two parallel agents that build backend and frontend simultaneously, then integrate.

## Prerequisites Check

1. Read `plan.md` — extract backend tasks and frontend tasks
2. Read `SYSTEM-DESIGN.md` — extract API contract (endpoints, request/response shapes)
3. Verify scaffold exists: `backend/app/main.py` and `frontend/src/App.tsx`

If any missing, tell user to run `/interview-kickoff` first.

Additional instructions: $ARGUMENTS

## Step 1: Create API Contract File

Before launching agents, create `API-CONTRACT.md` from SYSTEM-DESIGN.md endpoints. This is the shared contract both agents must follow:

```markdown
# API Contract
## Base URL: http://localhost:8000/api

### [Resource] Endpoints
- METHOD /path
  - Request: { field: type }
  - Response: { field: type }
  - Status codes: 200, 400, 404, 500
```

## Step 2: Launch Parallel Agents

Launch TWO agents simultaneously using the Agent tool with `isolation: "worktree"`:

### Agent 1: Backend Builder
```
You are building the FastAPI backend for an interview POC.

CONTEXT:
- Read plan.md for your tasks
- Read SYSTEM-DESIGN.md for data model and architecture
- Read API-CONTRACT.md for exact endpoint specs

YOUR TASKS (from plan.md backend section):
1. Implement all SQLAlchemy models in backend/app/models.py
2. Implement Pydantic schemas in backend/app/schemas.py
3. Implement all API routes in backend/app/routes/
4. Wire routes into backend/app/main.py
5. Add CORS middleware for http://localhost:5173
6. Seed sample data for demo

RULES:
- Follow API-CONTRACT.md exactly — frontend depends on it
- Use SQLite for database (no external deps)
- Every endpoint must work — test with curl mentally
- Add basic error handling (try/except, HTTP exceptions)
- No authentication unless plan.md says so
- No tests — this is a 30-min MVP
- Commit when done: "feat: implement backend API endpoints"
```

### Agent 2: Frontend Builder
```
You are building the React + TypeScript frontend for an interview POC.

CONTEXT:
- Read plan.md for your tasks
- Read SYSTEM-DESIGN.md for UI requirements
- Read API-CONTRACT.md for exact endpoint specs

YOUR TASKS (from plan.md frontend section):
1. Set up API client in frontend/src/api/client.ts (axios, base URL http://localhost:8000/api)
2. Create TypeScript types in frontend/src/types/index.ts matching API-CONTRACT.md
3. Build page components in frontend/src/pages/
4. Build reusable UI components in frontend/src/components/
5. Set up routing in App.tsx (react-router-dom)
6. Wire up API calls with loading/error states

RULES:
- Follow API-CONTRACT.md exactly — backend implements these endpoints
- Use Tailwind CSS for styling (or inline styles if Tailwind not set up)
- Functional components + hooks only
- useState/useEffect for state — no Redux or Zustand
- Show loading spinners and error messages
- Make it look presentable — this is for a demo
- No tests — this is a 30-min MVP
- Install needed deps: npm install axios react-router-dom
- Commit when done: "feat: implement frontend UI components"
```

## Step 3: Integration (after both agents complete)

Once both agents finish:

1. Check if worktree branches have conflicts:
   ```bash
   git merge --no-commit --no-ff <backend-branch>
   git merge --no-commit --no-ff <frontend-branch>
   ```

2. If no conflicts (likely — they touch different directories), merge both:
   ```bash
   git merge <backend-branch> -m "feat: merge backend implementation"
   git merge <frontend-branch> -m "feat: merge frontend implementation"
   ```

3. Verify integration:
   - Check frontend API calls match backend routes
   - Check TypeScript types match Pydantic schemas
   - Fix any mismatches between API contract implementations

4. Quick smoke test:
   ```bash
   cd backend && pip install -r requirements.txt && cd ..
   cd frontend && npm install && cd ..
   docker-compose up --build -d
   # or run individually if docker not ready
   ```

5. Final commit:
   ```bash
   git add -A
   git commit -m "feat: integrate backend and frontend"
   ```

## Step 4: Docker Verification

Ensure docker-compose.yml works:
```bash
docker-compose up --build
```

If it fails, fix issues and commit:
```bash
git add -A
git commit -m "fix: docker-compose configuration"
```

## RULES
- Both agents MUST use API-CONTRACT.md as source of truth
- Backend and frontend touch different directories — no conflicts expected
- If an agent fails, fix manually rather than re-running
- Total time budget: 10-15 minutes for parallel build + 5 minutes for integration
- Commit after each major milestone
