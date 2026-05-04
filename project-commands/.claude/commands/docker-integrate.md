---
description: Containerize backend and frontend with Docker Compose. Run after MVP is tested locally with /parallel-build.
argument-hint: Optional instructions (e.g. "add postgres container" or "use nginx reverse proxy")
---

# Docker Integration

You are packaging a working MVP into Docker containers. The app should already be running locally before using this command.

## Prerequisites Check

1. Verify backend runs: `backend/app/main.py` exists with working routes
2. Verify frontend runs: `frontend/src/App.tsx` exists with working components
3. Verify MVP was tested locally first

If not working locally, tell user to fix local issues before containerizing.

Additional instructions: $ARGUMENTS

## Step 1: Backend Dockerfile

Create `backend/Dockerfile`:
- Python 3.11-slim base
- Install dependencies from requirements.txt
- Copy app code
- Expose port 8000
- CMD: uvicorn app.main:app --host 0.0.0.0 --port 8000

## Step 2: Frontend Dockerfile

Create `frontend/Dockerfile`:
- Node 20-alpine base
- Install dependencies from package.json
- Copy source and build
- Serve with lightweight server (e.g. `serve` or nginx)
- Expose port 3000

## Step 3: Docker Compose

Create `docker-compose.yml`:
- backend service on port 8000
- frontend service on port 3000
- Shared network
- Environment variables for API URLs
- Add database service if needed (postgres/sqlite volume)

## Step 4: Verify

1. Run `docker-compose up --build`
2. Test end-to-end flow matches local behavior
3. Fix any container-specific issues (networking, env vars, paths)

## Step 5: Commit

```bash
git add -A
git commit -m "feat: add Docker containerization"
```
