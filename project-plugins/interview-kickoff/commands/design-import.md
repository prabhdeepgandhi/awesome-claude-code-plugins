---
description: Read a text-based system design description or Excalidraw image (.excalidraw, .excalidraw.png, .png, .jpg) and generate/update SYSTEM-DESIGN.md with ASCII line diagrams. Supports whiteboard photos, architecture sketches, and text descriptions.
argument-hint: Path to image file OR text description of system (e.g. "@ design.excalidraw.png" or "3-tier web app with cache layer")
---

# Design Import

You are a system design interpreter. Your job is to read a visual or textual system design and produce a clean SYSTEM-DESIGN.md with ASCII architecture diagrams.

**Input:** $ARGUMENTS

## Step 1: Interpret the Design

### If input is an IMAGE file (Excalidraw, PNG, JPG, screenshot, whiteboard photo):
1. Read the image file using the Read tool
2. Identify all components: services, databases, queues, caches, load balancers, clients, external APIs
3. Identify all connections: arrows, lines, data flow direction
4. Identify labels: endpoint names, protocol annotations, port numbers
5. Note any groupings: microservice boundaries, network zones, Docker containers

### If input is TEXT description:
1. Parse the description for components and relationships
2. Infer standard architecture patterns (3-tier, microservices, event-driven, etc.)
3. Fill in obvious gaps (e.g. "web app with database" implies HTTP between client and server)

### If SYSTEM-DESIGN.md already exists:
1. Read it first
2. Merge new information — don't overwrite existing detail
3. Upgrade text descriptions to ASCII diagrams where possible

## Step 2: Generate ASCII Architecture Diagrams

Create diagrams using box-drawing characters. Follow these patterns:

### Main Architecture Diagram
```
┌─────────────┐     HTTP      ┌─────────────────┐     SQL      ┌──────────────┐
│   Browser    │──────────────▶│  FastAPI Server  │────────────▶│   Database   │
│  (React SPA) │◀──────────────│   :8000          │◀────────────│  (SQLite)    │
└─────────────┘    JSON        └─────────────────┘    ORM       └──────────────┘
                                       │
                                       │ (optional)
                                       ▼
                               ┌──────────────┐
                               │  Redis Cache  │
                               └──────────────┘
```

### Use these box-drawing characters:
- Boxes: `┌ ─ ┐ │ └ ┘`
- Arrows: `▶ ◀ ▲ ▼ ──▶ ◀── ───`
- Connectors: `┬ ┴ ├ ┤ ┼`
- Double lines for boundaries: `╔ ═ ╗ ║ ╚ ╝`

### Data Flow Diagram (if multiple flows exist)
```
User Request Flow:
  Client ──▶ API Gateway ──▶ Auth Middleware ──▶ Route Handler ──▶ DB Query ──▶ Response

Background Job Flow:
  Scheduler ──▶ Task Queue ──▶ Worker ──▶ DB Write ──▶ Notification
```

### Docker Compose Diagram (if using Docker)
```
╔══════════════════════════════════════════════╗
║  docker-compose                              ║
║                                              ║
║  ┌──────────┐  :8000   ┌──────────┐         ║
║  │ backend  │◀────────▶│ frontend │  :5173   ║
║  │ (FastAPI) │          │ (React)  │─────▶ 🌐║
║  └────┬─────┘          └──────────┘         ║
║       │                                      ║
║       ▼                                      ║
║  ┌──────────┐                                ║
║  │   db     │  :5432                         ║
║  │ (Postgres)│                               ║
║  └──────────┘                                ║
╚══════════════════════════════════════════════╝
```

### Entity Relationship Diagram
```
┌──────────────┐       ┌──────────────┐
│    User      │       │    Post      │
├──────────────┤       ├──────────────┤
│ id      (PK) │──┐    │ id      (PK) │
│ email        │  │    │ title        │
│ name         │  └───▶│ user_id (FK) │
│ created_at   │  1:N  │ content      │
└──────────────┘       │ created_at   │
                       └──────────────┘
```

## Step 3: Write SYSTEM-DESIGN.md

Generate or update the file with this structure:

```markdown
# System Design: [Project Name]

## Architecture Overview

[Main ASCII architecture diagram here]

## Components

### [Component 1]
- **Role**: What it does
- **Tech**: Technology used
- **Port**: Exposed port
- **Key responsibilities**: Bullet list

### [Component 2]
...

## Data Model

[ER diagram here]

### Entities
| Entity | Fields | Type | Constraints |
|--------|--------|------|-------------|
| User   | id     | int  | PK, auto    |
| ...    | ...    | ...  | ...         |

## API Endpoints

| Method | Path | Description | Request | Response |
|--------|------|-------------|---------|----------|
| GET    | /api/items | List items | - | Item[] |
| POST   | /api/items | Create item | {name, ...} | Item |
| ...    | ... | ... | ... | ... |

## Data Flow

[Data flow diagram here]

## Infrastructure

[Docker compose diagram here]

### Services
| Service | Image | Port | Depends On |
|---------|-------|------|------------|
| backend | python:3.11 | 8000 | db |
| frontend | node:20 | 5173 | backend |

## Sequence Diagrams (Key Flows)

### [Flow Name]
```
Client          Backend         Database
  │                │               │
  │── POST /api ──▶│               │
  │                │── INSERT ────▶│
  │                │◀── row ───────│
  │◀── 201 ────────│               │
  │                │               │
```

## Scalability Notes
- What would change at 10x scale
- What would change at 100x scale
- Current bottlenecks and mitigation strategies
```

## Step 4: Verify

After writing, read back SYSTEM-DESIGN.md and verify:
- All components from input are represented
- All connections/arrows are captured
- Diagrams render correctly in monospace font
- No broken box-drawing characters

## RULES
- ASCII diagrams MUST use box-drawing characters (┌─┐│└┘), not plain dashes
- Every component gets a box, every connection gets an arrow
- Label arrows with protocol/data type (HTTP, SQL, gRPC, JSON, etc.)
- Keep diagrams under 80 chars wide for terminal readability
- If image is blurry or ambiguous, state assumptions explicitly
- Preserve any existing content in SYSTEM-DESIGN.md that isn't being replaced
