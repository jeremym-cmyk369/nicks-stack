# Mandile AI Business Harness — development foundation

Status: **planning / non-production**. This directory is an adaptation plan for the `nickvasilescu/nicks-stack` fork, not a statement that any agent or integration has been deployed.

## Purpose
Build a managed business-operations service, not an unrestricted "AI employee." The first demonstration is an **Automotive Estimate Follow-Up Operator** that reviews fictional open estimates, prepares suggested follow-ups, routes decisions for human approval, and reports outcomes.

## Architecture
- **Mandile AI Workforce Operator:** workflow discovery, baseline/value analysis, agent coordination, monitoring, exception routing, reporting. Do **not** give this parent unrestricted credentials across clients.
- **Isolated client execution:** separate client credentials, data, inbox, knowledge base, audit logs, workflow configuration, and recovery plan. A dedicated virtual desktop is optional unless the approved task needs desktop access.
- **Specialized workflow agent:** access limited to its explicitly approved sources and actions; starts with **read and draft** rather than send or modify permissions.
- **Integration preference:** deterministic checks and supported APIs first; MCP and browser/desktop control only where justified and tested.

## First demonstration (fictional records only)
1. Ingest permitted synthetic estimate records.
2. Identify incomplete records, already-contacted cases, and records needing review.
3. Build a proposed action and draft internal/customer follow-up.
4. Route external communications and sensitive operations to a human approval queue.
5. Require an approval record associated with the exact action payload.
6. Log the resulting simulated action and every exception.
7. Produce a test summary showing processed, drafted, reviewed, and skipped records.

## Pilot acceptance criteria
- No live credentials, customer data, or outgoing messages in the synthetic demonstration.
- Repeatable sample input and deterministic expected output.
- Fail closed on ambiguous status, absent consent, unavailable permissions, duplicate work, and approval failures.
- Idempotency or a documented duplicate-prevention check before each write.
- Auditable inputs, proposed outputs, approvals, attempts, and verified results.
- Unit/integration tests for ordinary, missing-data, duplicate, permission-denied, retry, and manual-review scenarios.
- Separate measurement plan covering time spent, response delay, exceptions, and completed follow-up.
- No claims of ROI or production performance until measured.

## Build gates
1. Inventory dependencies, required services, and each component's license.
2. Review `docs/mandile/SECURITY_REVIEW.md` and confirm actual Hermes config semantics on the intended version.
3. Prepare an isolated development environment, not the existing Mandile SEO website or active Hermes installation.
4. Add simulated workflow tests and run them locally/CI.
5. Connect a dedicated **test** inbox in draft-only mode, with a scoped secret store.
6. Enable observable error handling, backups, and rollback.
7. Approve client data access and execution separately from development.
8. Only then evaluate a paid 30-day pilot; the proposed $5,000 fee is a business hypothesis, not an established price.

## Boundaries
- **Do not** attach payment cards, make purchases, send external messages automatically, or bypass MFA.
- **Do not** paste secrets into chat, source files, examples, or logs.
- Do not assume this fork has been deployed on Orgo/Hostinger or that any MCP integration is connected.
- Preserve Nick Vasilescu's MIT license and notice, and check third-party licenses and service terms separately.
- `main` remains upstream-equivalent until changes are reviewed and merged.

See [Nick's Stack README](../../README.md), [LICENSE](../../LICENSE), and [Security Review](SECURITY_REVIEW.md).
