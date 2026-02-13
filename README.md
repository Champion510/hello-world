# Capital Routing OS MVP with Codex

This guide turns a Capital Routing OS concept into executable code using Codex in iterative, testable slices.

## 1) Define MVP Scope First

Avoid asking for the entire system in one shot. Build in slices:

1. Backend API scaffold
2. Data models (trust graph, founders, investors, connectors)
3. Routing engine stub with scoring function
4. Daily dashboard endpoint
5. Basic frontend (Next.js/React)

### Planning Prompt

```text
You will act as a senior full-stack engineer.
I’m building an MVP of an AI-powered capital routing OS.

Phase 1 backend:
- Express (Node.js) API
- PostgreSQL database
- REST endpoints for founders, investors, connectors
- Deal probability engine stub (returns score placeholder)
- Trust graph model

Write:
1) A high-level architecture plan
2) List of API endpoints
3) Data models with fields
4) Folder structure for project
5) Prompts for next step code generation
```

## 2) Generate Database Schema

Use a dedicated schema step after planning.

### Schema Prompt

```text
Based on this data model plan:
- Founder
- Investor
- Connector
- TrustEdge (weights)
- DealProbability

Generate PostgreSQL schema DDL statements.
Include constraints and indexes for fast graph traversal.

Expect tables with id, entity_type, vector embeddings, and edge weights.
```

## 3) Build Backend API Incrementally

Implement endpoints in small batches.

### API Scaffold Prompt

```text
Generate Node.js Express code for:
POST /founders
GET /founders/:id
POST /investors
GET /investors/:id
POST /connectors
GET /connectors/:id

Each endpoint should use Sequelize (or Prisma) to interact with PostgreSQL.
Include validation and basic error handling.
```

## 4) Implement Core Engines in Stages

### Deal Probability Engine (Stub)

Create `dealProbability.js` with:
- Inputs: founder profile, investor profile, weighted features (thesis match, stage, check size)
- Output: score between 0 and 1
- Unit tests with mock data

### Trust Graph Routing

Implement a minimal routing function:
- Query graph edges
- Compute best intro path (BFS or weighted traversal)
- Return best connector path + score

## 5) Add AI Layer (Embeddings + Similarity)

### AI Integration Prompt

```text
Add backend service that:
1) Creates embeddings for founder/investor profiles
2) Stores vectors in PostgreSQL (pgvector)
3) Computes semantic similarity for thesis alignment

Use OpenAI embeddings API and write async functions.
Include tests.
```

## 6) Build Minimal Frontend

### Next.js UI Prompt

```text
Generate a Next.js pages/ directory with:
- /dashboard showing 3 ranked deals
- /founders/new (create founder)
- /investors/new (create investor)
Use Tailwind CSS.
Include API calls to backend.
```

## 7) Steer Codex with Fast Iteration

Treat Codex as a collaborator and correct drift quickly:

- “You misunderstood. Focus on…”
- “Revise code to use X instead of Y…”

Prefer iterative refinement over one-shot generation.

## 8) Build/Commit Workflow

Recommended sequence:

1. Architecture plan
2. Schema
3. Backend endpoints
4. Routing engine
5. AI integration
6. UI
7. Test and fix

## Practical Prompting Tips

- Start with comments/docstrings to anchor structure.
- Provide examples/tests so output matches expected patterns.
- Break large asks into smaller prompts.

## Summary Playbook

1. Describe architecture first.
2. Prompt for schema.
3. Build backend slice by slice.
4. Add AI scoring module.
5. Generate frontend screens.
6. Iterate with guided corrections.

This plan-first, generate-in-slices workflow improves correctness, testability, and speed.
