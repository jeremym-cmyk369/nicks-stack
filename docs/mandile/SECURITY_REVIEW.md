# Mandile AI Business Harness — security and deployment review

**Basis:** inspected `files/config.yaml` and `LICENSE` on fork `main` (upstream-aligned commit `90b9975c5391591e98565d20d33554a6b91f2f85`). This document is an evidence checklist, **not** a hardened production configuration or security certification.

## Verified source configuration (requires review before a client deployment)

| Source field | Checked value | Production gate |
| --- | --- | --- |
| `approvals.mode` | `false` | Verify supported approval modes and enable explicit human-approval handling for sensitive writes. |
| `approvals.mcp_reload_confirm` | `false` | Require review of MCP connection changes when supported. |
| `approvals.destructive_slash_confirm` | `false` | Validate and enable appropriate destructive-action confirmation. |
| `hooks_auto_accept` | `true` | Disable or constrain automatic hook acceptance after confirming version semantics. |
| `tool_loop_guardrails.hard_stop_enabled` | `false` | Test and enable hard stops for repeated failures/no progress. |
| `updates.pre_update_backup` | `false` | Enable validated pre-update backups; test restoration. |
| `agent.verify_on_stop` | `false` | Add verified outcomes and action receipts; inspect the supported option. |
| `secrets.onepassword.enabled` | `false` | Not itself a defect: template intentionally ships without a secret-manager login. Configure secure secret management for each deployment. |

**Important:** Do not flip these fields blindly in the template. Validate parameter types, authentication behavior, and compatibility against the exact installed Hermes version; add tests that exercise the intended controls.

## Isolation and minimum permissions
- Unique tenant/workspace, separate credentials, inbox, logs, and service accounts for each client.
- Parent orchestrator has no universal cross-tenant production credentials.
- Limit each child agent to one defined workflow and approved connectors.
- Read-only/draft-only initially. Per-action human approval for customer messages, money, deletions, access changes, and legally significant decisions.
- No payment card or unsupervised purchasing in the first release.
- No bypass of MFA, application security controls, or provider terms.
- No credential injection via conversational prompts or public CI artifacts.

## Reliability and audit
- Keep an immutable or tamper-evident record of proposed action, approval, execution attempt, and independently verified outcome.
- Handle retries with idempotency keys and stop after repeated failures.
- Have owner-visible incident notifications, an emergency stop, documented rollback, and tested recovery from backups.
- Record only necessary client data and establish retention and deletion policies.
- Review traces for personal/confidential data before exporting them to a third-party observability service.

## Compatibility and deployment checks
- Confirm actual build/runtime version; repository README describes a particular Nick's Stack template rather than the currently running local Hermes installation.
- Keep Nick's Stack MIT notice and identify the separate licenses of Hermes, plugins, cloud desktop provider, and external APIs.
- Validate infrastructure and subscription costs before promising any always-on service.
- Do not represent source-code review as a deployment, live security test, or operational success.
- Check branch protections and CI before merging any code intended for client environments.

## Exit criteria before production
[ ] Full secret/dependency/license inventory
[ ] Exact runtime version and config schema validated
[ ] Approval, stopping, backup and recovery controls tested
[ ] Client boundary tested with deliberately mismatched tenant credentials
[ ] Synthetic workflow cases passing
[ ] Authorized test inbox, draft-only and isolated
[ ] Logs, alerts, rate/cost limits, and manual kill-switch verified
[ ] Legal/contractual data handling and client authorization documented
[ ] Written go/no-go approval

**Current status:** None of the boxes above are presumed complete merely because this document exists.
