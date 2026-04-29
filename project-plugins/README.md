# Project-Level Plugins — 30-Min Interview POC

Install these in your project's `.claude/plugins/` directory.

## Plugins

| Plugin | Type | Command/Agent | What it does |
|--------|------|---------------|-------------|
| **interview-kickoff** | Command | `/kickoff <idea>` | Full kickoff: requirements → system design → plan.md → scaffold |
| **parallel-build** | Command | `/parallel-build` | Launches backend + frontend agents in parallel worktrees |
| **rapid-prototyper** | Agent | Auto-triggered | FastAPI + React + Docker MVP scaffolding |
| **deployment-engineer** | Agent | Auto-triggered | Docker + docker-compose setup |
| **feature-dev** | Command | `/feature-dev <feature>` | Streamlined 4-phase feature development |

## Workflow

```
/kickoff "build a URL shortener with analytics"
  → generates SYSTEM-DESIGN.md, plan.md, project scaffold

/parallel-build
  → spawns backend + frontend agents in parallel
  → auto-merges when both complete

/feature-dev "add click tracking analytics"
  → builds individual features fast

/double-check
  → validates everything works

/commit-push-pr
  → ships it
```

## Installation

```bash
# In your new project directory:
mkdir -p .claude/plugins

# Copy all project plugins
cp -r path/to/project-plugins/* .claude/plugins/
```

## What's Reused vs New

| Plugin | Source | Changes |
|--------|--------|---------|
| interview-kickoff | **NEW** — combines discuss + plan + rapid-prototyper + sprint-prioritizer |  |
| parallel-build | **NEW** — combines create-worktrees + feature-dev + studio-producer |  |
| rapid-prototyper | Tweaked from original | Stack changed to FastAPI+React+Docker, removed social/viral features |
| deployment-engineer | Tweaked from original | Simplified to Docker-only, removed K8s/cloud/CI |
| feature-dev | Trimmed from original | 7 phases → 4 phases, removed exploration + clarifying questions |
