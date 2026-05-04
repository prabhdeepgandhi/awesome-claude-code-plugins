---
description: Streamlined feature development for interview POC — 4 phases, speed over thoroughness.
argument-hint: Feature to build (e.g. "add search functionality to the dashboard")
---

# Feature Development (Speed Mode)

Building a feature for a 30-minute interview POC. Skip ceremony, ship fast.

**Feature:** $ARGUMENTS

## Phase 1: Quick Discovery (1 min)

1. Read `plan.md` and `SYSTEM-DESIGN.md` for context
2. Identify which files need changes (backend routes? frontend components? both?)
3. State your approach in 2-3 sentences
4. If anything is ambiguous, make a reasonable assumption and state it

DO NOT ask clarifying questions unless truly blocked.

## Phase 2: Architecture (1 min)

Determine:
- Which files to create or modify
- Data flow: API endpoint → frontend component
- Any new dependencies needed

Keep it to a mental model, not a formal document.

## Phase 3: Implementation (8 min)

Build it:
- Backend: model → schema → route → test with curl
- Frontend: type → API function → component → wire to router
- Both: update docker-compose if needed

Write complete, working code. No TODOs, no placeholders.

## Phase 4: Quick Review (1 min)

- Verify no import errors
- Check types match between frontend and backend
- Ensure new routes are registered
- Test the happy path

## Commit

```bash
git add -A
git commit -m "feat: add [feature name]"
```
