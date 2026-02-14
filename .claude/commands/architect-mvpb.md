# Phase 2: Architecture & Technical Design

You are the **Architect** (led by the PM). Your goal is to produce `CLAUDE.md`, `docs/ARCHITECTURE.md`, and `README.md` that define *how* the product will be built.

Read `CLAUDE.md`, `.planning/STATE.md`, `.planning/DECISIONS.md`, and `docs/PRODUCT_SPEC.md` first.

$ARGUMENTS

## Step 1: Tech Stack Decision

**IMPORTANT: Use the `AskUserQuestion` tool to collect tech stack decisions interactively — NEVER display a big table of options.** Ask 1–4 questions at a time with recommended options. Let the human select or type a custom response.

**Round 1 — Core stack:**
- "Frontend framework?" (header: "Frontend") — Options: "Next.js (Recommended)", "React + Vite", "SvelteKit", "Nuxt"
- "Styling approach?" (header: "Styling") — Options: "Tailwind CSS (Recommended)", "CSS Modules", "Styled Components"
- "Backend framework?" (header: "Backend") — Options: "Next.js API Routes (Recommended)", "Express.js", "FastAPI (Python)", "Hono"

**Round 2 — Data & auth:**
- "Database?" (header: "Database") — Options: "PostgreSQL (Recommended)", "MySQL", "SQLite", "MongoDB"
- "ORM / query layer?" (header: "ORM") — Options: "Prisma (Recommended)", "Drizzle", "TypeORM", "Raw SQL"
- "Authentication?" (header: "Auth") — Options: "NextAuth.js (Recommended)", "Lucia Auth", "Custom JWT", "Clerk"

**Round 3 — AI & infra:**
- "AI provider & model?" (header: "AI Model") — Options: "OpenAI GPT-4o (Recommended)", "Anthropic Claude", "Both (multi-provider)"
- "Hosting platform?" (header: "Hosting") — Options: "Vercel (Recommended)", "Railway", "AWS", "Fly.io"

**Round 4 — Services (only ask if relevant to the product):**
- "Email service?" (header: "Email") — Options: "Resend (Recommended)", "SendGrid", "None for MVP"
- "CI/CD?" (header: "CI/CD") — Options: "GitHub Actions (Recommended)", "Vercel Auto-deploy", "GitLab CI"

After collecting choices, summarize the full stack and ask for final confirmation. Justify each choice briefly.

> ⚠️ If any choice requires an API key not yet provided, follow the Service Keys Protocol: explain what's needed, why, propose a fallback if denied, wait for confirmation.

## Step 2: Architecture Document

Create `docs/ARCHITECTURE.md` with:

1. **System Overview Diagram** (Mermaid or ASCII)
2. **Component Breakdown** — Frontend, backend, database, external services
3. **Data Model / Schema** — Complete ER diagram. Every entity, field, type, relationship.
4. **API Design** — Every endpoint: method, path, request/response shape, auth requirement. Group by resource.
5. **Auth Flow** — Registration → verification → login → refresh → logout
6. **Data Flow Diagrams** — Top 3 core workflows
7. **Error Handling Strategy** — Global error boundary, centralized handler, structured error format, logging
8. **Environment & Configuration** — All environments, env var naming, secrets management, `.env.example`
9. **Folder Structure** — Proposed layout with explanations
10. **AI Architecture** — Critical section:
    - AI Service Layer (centralized, all calls go through it)
    - Model Selection per tier
    - Prompt Management (prompts as code, versioned)
    - Chatbot Architecture (system prompt, memory storage, user context injection, topic guardrails)
    - Fallback Strategy for every AI feature
    - Structured Outputs for Tier 1 (JSON mode / function calling, schema validation)
    - Prompt Injection Defense (delimiter tokens, structured messages, classification step, output validation)
    - AI Response Caching (cacheable queries, TTL per use case)
    - Cost Estimation (~X calls/user/day × ~Y cost = ~Z monthly)
    - Token & Cost Tracking schema
11. **Production Deployment Architecture** — Domain, SSL, deploy/rollback scripts, zero-downtime strategy, health checks, backups

## Step 3: Tooling Augmentation (MCP Servers & Skills)

Review the architecture. Identify MCP servers and skill files that would help. Each proposal needs: what it does, why it helps, fallback without it. Present consolidated list to human for approval.

## Step 4: CLAUDE.md

Write the project instruction file with: project overview, team structure, tech stack, architecture reference, 24 golden rules (including the mandatory parallel dispatch rule), testing strategy, deployment info, repository links. This file is read every session — it must be concise and authoritative.

## Step 5: README.md

Create README with: what the product is, who it's for, architecture summary, prerequisites, local setup, test commands, deploy overview, env var reference, links to docs.

## Gate — 🧑 Human

Present architecture to the human. The gate requires:

- [ ] `CLAUDE.md` is complete and reviewed.
- [ ] `docs/ARCHITECTURE.md` is complete with data model, API design, AI architecture, and all sections.
- [ ] `README.md` is complete.
- [ ] Human has approved tech stack, data model, API design, and AI architecture.
- [ ] MCP servers proposed, approved/denied, configured (or fallbacks documented).
- [ ] Skills proposed, approved/denied, downloaded to `skills/`.

Once approved, update `.planning/STATE.md` and `.planning/DECISIONS.md` with key decisions. Log: **"Approved — moving to Task Breakdown & Planning."**

## ➡️ Auto-Chain

This phase ends with a 🧑 Human gate. **STOP and wait** for the human to explicitly approve the gate checklist. Once approved, immediately begin executing the next phase by reading and following `.claude/commands/plan-mvpb.md`.
