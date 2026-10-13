# MDDT Agent OS — current state

2026-10-13

Goal: build a maintained downstream Agent OS on DeepSeek Harness with auditable data handling and workspace-owned instructions visible in the application.

- Source: upstream DeepSeek Harness (MIT); origin is the MDDT fork. Product branch: codex/mddt-agent-os; master retains the upstream baseline.
- OS-02 source fixes (see OS-02-PRIVACY-SPEC.md) disable Session-log upload, plugin inventory, OTel feedback export and Desktop analytics by default; DeepSeek installation/Session headers require explicit opt-in. Ordinary requests to the selected model provider remain. Source-built egress qualification is still pending; branding, installed applications and live user configuration are unchanged.
- Security review: AUDIT_2026-10-12.md and evidence files; 12 qualified lockfile advisories. Read/credential isolation, dependencies and updater feed remain open; installed app excluded at owner request.
- Verification: locked dependencies installed without scripts after owner-approved network access. Host/Client/Web builds, typecheck, 326 focused tests, Web opt-in upload toggle (installed Chromium), SDK upload snapshot with explicit opt-in, lint (one unrelated warning), and 43/43 documentation gates passed. Additional Desktop analytics no-emission test and final doc-sync rerun passed. Independent reviews found no scoped blocker; broad snapshot suite failed on other replay fixtures. No provider model calls ran.
- Next: push source changes only, not install or replace Desktop. For a Desktop pilot use an isolated development home and browser data, inspect inherited environment and `DSH_AGENTS_HOME`, and account for the macOS `dsh://` handler side effect; avoid launching a packaged fork with the existing live home. Qualify source-built outbound traffic with synthetic canaries before confidential workloads. Read/credential isolation, updater identity/feed, dependency advisories and OS-03 workspace UI remain separate tasks.
