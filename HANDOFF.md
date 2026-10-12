# MDDT Agent OS — current state

2026-10-12

Goal: build a maintained downstream Agent OS on DeepSeek Harness with auditable data handling and workspace-owned instructions visible in the application.

- Source: deepseek-ai/deepseek-harness, MIT. Initial baseline: d743267388641bc76f17c45ce8b4c231aed1d32c.
- Origin: aleksundervolkov/mddt-agent-os. Upstream remote configured. Product branch: codex/mddt-agent-os; master remains the original baseline.
- MDDT_AGENT_OS.md records upstream synchronization, security/egress audit, workspace settings/editor and a possible separate upstream contribution.
- Runtime code, branding, dependencies and existing installed applications are unchanged. No source build, security audit, deployment or automatic synchronization has been performed.
- Next: audit the pinned source and installed artifact's outbound paths, then implement OS-03 as a focused UI/API change with workspace role inheritance and source-conflict tests. OS-04 remains a candidate, not a published PR.
