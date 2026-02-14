# Phase 6: Deployment & Launch Prep

You are the **DevOps** lead (coordinated by PM). Your goal is to get the application running in production with monitoring.

Read `CLAUDE.md`, `.planning/STATE.md`, `.planning/DECISIONS.md`, and `docs/ARCHITECTURE.md` first.

$ARGUMENTS

## Step 1: Production Deployment Scripts

Create production-ready scripts:

- **`scripts/deploy.sh`** — Test → lint → build → migrate → deploy → smoke test → output summary (version, timestamp, commit hash). Abort on any failure.
- **`scripts/deploy-rollback.sh`** — Identify previous version → revert → verify backward-compatible migrations → smoke test.
- **`scripts/seed.sh`** — Seed admin account + sample data. Configurable per environment.

Both deploy scripts must be tested end-to-end before the gate.

## Step 2: Production Domain & Infrastructure

1. Configure the production domain.
2. Set up DNS records.
3. Configure SSL/TLS (auto-renewal).
4. Set up CI/CD pipeline:
   - Push to `develop`: tests, lint, type-check.
   - Merge to `main`: tests → build → deploy.
5. Configure production environment variables (including AI API keys).
6. Set up monitoring / error tracking (Sentry or equivalent).
7. Set up health check endpoint (`/api/health`) — verifies app running, DB connected, AI API reachable.
8. Configure structured JSON logging for production.
9. Set up AI cost monitoring alerts.

## Step 3: Pre-Launch Checklist

Verify each item:

- [ ] All tests pass in CI.
- [ ] Production domain is live and resolves.
- [ ] SSL certificate is valid and auto-renewing.
- [ ] `scripts/deploy.sh` executes successfully end-to-end.
- [ ] `scripts/deploy-rollback.sh` has been tested.
- [ ] Production env vars configured (including `OPENAI_API_KEY`).
- [ ] Database migrated and seeded.
- [ ] Health check responds at `https://[domain]/api/health`.
- [ ] Error tracking receiving test events.
- [ ] Security headers set.
- [ ] Rate limiting active (including AI endpoints).
- [ ] AI API calls working in production (test one core feature).
- [ ] AI cost alerts configured.
- [ ] Admin account created.
- [ ] `.env.example` up to date.
- [ ] README has correct setup and deploy instructions.

## Step 4: Demo Script

Create `docs/DEMO.md`:

1. **Setup instructions** — How to get the demo environment running.
2. **Demo walkthrough** — Step-by-step: Registration → Core AI feature → Smart suggestions → Chatbot → Profile → Admin panel → AI usage dashboard.
3. **Talking points** — What to highlight at each screen.
4. **Known limitations** — What's not in the MVP.
5. **Sample data** — Seed data that makes the demo compelling.

## Gate — 🧑 Human

Present to the human:

- [ ] Application deployed and accessible at production domain.
- [ ] Deploy and rollback scripts work.
- [ ] Monitoring and AI cost alerts active.
- [ ] Demo script written and tested.
- [ ] Human has walked through the demo.

Once approved, update STATE.md. Log: **"Approved — moving to Iteration & Backlog. The product is live!"**

## ➡️ Auto-Chain

This phase ends with a 🧑 Human gate. **STOP and wait** for the human to explicitly approve the gate checklist. Once approved, immediately begin executing the next phase by reading and following `.claude/commands/iterate-mvpb.md`.
