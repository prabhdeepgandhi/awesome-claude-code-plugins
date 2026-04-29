---
description: Streamlined feature development for interview POC — 4 phases instead of 7. Speed over thoroughness.
argument-hint: Feature to build (e.g. "add search functionality to the dashboard")
---

# Feature Development (Speed Mode)

Building a feature for a 30-minute interview POC. Skip ceremony, ship fast.

**Feature:** $ARGUMENTS

## Phase 1: Quick Discovery (1 min)

1. Read `plan.md` and `SYSTEM-DESIGN.md` for context
2. Identify which files need changes (backend routes? frontend components? both?)
3. State your approach in 2-3 sentences — no long writeups
4. If anything is ambiguous, make a reasonable assumption and state it

DO NOT ask clarifying questions unless truly blocked. Time is limited.

---

## Phase 2: Architecture Sketch (1 min)

Launch a code-architect agent to quickly determine:
- Which files to create or modify
- Data flow: API endpoint → frontend component
- Any new dependencies needed

Keep it to a mental model, not a formal document.

---

## Phase 3: Implementation (5-8 min)

Build the feature end-to-end:

### Backend (if needed)
1. Add/modify SQLAlchemy model
2. Add/modify Pydantic schema
3. Add/modify FastAPI route
4. Wire into main.py if new router

### Frontend (if needed)
1. Add TypeScript types
2. Add API call function
3. Build/modify React component
4. Wire into routing/page

### Integration
- Verify frontend API calls match backend routes
- Check types match between Pydantic schemas and TypeScript interfaces

---

## Phase 4: Quick Review (1 min)

Launch a code-reviewer agent (confidence threshold 80+) to check for:
- Broken imports
- Missing error handling on API calls
- Type mismatches
- Obvious bugs

Fix critical issues only. Skip style nits.

Commit: `feat: add [feature name]`

---

## RULES
- Total time budget: 10 min max per feature
- No tests
- No documentation beyond code comments
- No abstract patterns — direct implementation
- If stuck >3 min, simplify the approach
- Commit after each feature
