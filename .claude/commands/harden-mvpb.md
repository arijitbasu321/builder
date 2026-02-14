# Phase 5: Quality & Security Hardening

You are the **Security** lead (with QA co-lead, coordinated by PM). Your goal is a systematic review of the complete application for bugs, security vulnerabilities, UX issues, and missing edge cases.

Read `CLAUDE.md`, `.planning/STATE.md`, `.planning/DECISIONS.md`, `.planning/LEARNINGS.md`, and `docs/ARCHITECTURE.md` first.

$ARGUMENTS

## Step 1: Brainstorming Session

Review the entire application and log issues in the GitHub Project backlog. Use these labels:

- **`bug`**: Broken flows, incorrect behavior, race conditions
- **`feature`**: Missing expected functionality
- **`ui`**: Layout, responsiveness, accessibility, loading/empty/error states
- **`security`**: Vulnerabilities, missing validation, exposed data
- **`performance`**: Slow queries, re-renders, missing pagination
- **`dx`**: Missing types, unclear code, documentation gaps

**Use `AskUserQuestion` to ask the human which areas to prioritize** (header: "Focus areas") — Options: "Full audit (all categories)", "Security-first", "UX & polish priority". Let them select or provide custom focus.

## Step 2: Deep Security Audit

**Adversarial review technique:** Write your list of attack vectors BEFORE reading the code. Then verify each one.

1. **Auth & Sessions** — Password hashing (bcrypt/argon2), session expiry/refresh, failed login rate limiting, secure password reset.
2. **Authorization** — Every endpoint enforces auth. No privilege escalation. Resource ownership verified.
3. **Input Handling** — All inputs validated server-side. SQL injection protection. XSS protection. File upload validation.
4. **Data Protection** — PII encrypted at rest. All traffic HTTPS. No sensitive data in logs. CORS not `*` in production.
5. **Infrastructure** — Dependencies audited. No secrets in source/git history. Rate limiting on public endpoints. Security headers set.
6. **AI-Specific Security** (verify implementation matches ARCHITECTURE.md spec):
   - AI API keys not in client code, network responses, or logs
   - All AI calls route through backend service layer
   - Prompt injection defenses implemented (delimiter tokens, structured messages, output validation, classification step)
   - AI responses validated against schemas before use in business logic
   - Chatbot guardrails enforced server-side, resist bypass attempts
   - Per-user rate limits on AI endpoints
   - AI cost alerts configured
   - Conversation history scoped per-user (no cross-user leakage)
   - Chatbot cannot reveal system prompts or internal details

**Severity classification:**
- **Critical** — Blocks MVP. Must fix now.
- **High** — Blocks MVP. Must fix now.
- **Medium** — Log for post-launch. Document risk.
- **Low** — Log for post-launch.

Log every finding as a GitHub issue with label `security` and severity.

## Step 3: Resolve Critical & High Issues

Work through security and critical bug issues using the same task loop from Phase 4 (fresh context per task, branch per fix, test, review, merge).

## Gate — 🧑 Human

Present findings and resolution to the human:

- [ ] Security audit is complete and documented.
- [ ] All Critical and High issues are resolved.
- [ ] Full test suite still passes after fixes.
- [ ] Human has reviewed the remaining backlog and is comfortable with what's deferred.

Once approved, update STATE.md and DECISIONS.md. Log: **"Approved — moving to Deployment & Launch Prep."**

## ➡️ Auto-Chain

This phase ends with a 🧑 Human gate. **STOP and wait** for the human to explicitly approve the gate checklist. Once approved, immediately begin executing the next phase by reading and following `.claude/commands/deploy-mvpb.md`.
