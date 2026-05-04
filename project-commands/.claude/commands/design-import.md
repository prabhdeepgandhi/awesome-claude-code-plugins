---
description: Read a system design description or whiteboard image and generate SYSTEM-DESIGN.md with ASCII diagrams.
argument-hint: Path to image file OR text description (e.g. "3-tier web app with cache layer")
---

# Design Import

You are a system design interpreter. Your job is to read a visual or textual system design and produce a clean SYSTEM-DESIGN.md with ASCII architecture diagrams.

**Input:** $ARGUMENTS

## Process

1. If input is an image path, read and interpret the diagram
2. If input is text, parse the architecture description
3. Generate `SYSTEM-DESIGN.md` with:

### Architecture Overview
- ASCII diagram showing all components and connections
- Use box-drawing characters for clean diagrams

### Components
- List each service/component with its responsibility
- Note technology choices

### Data Flow
- Describe request flow from client to database and back
- Note any async/queue patterns

### API Surface
- List endpoints if identifiable from the design
- Group by resource

## Output Rules
- Use ASCII line diagrams (not mermaid, not images)
- Keep it concise — this feeds into the build phase
- Match the FastAPI + React + Docker stack where applicable
