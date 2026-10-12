# MDDT Agent OS

MDDT Agent OS is a downstream fork of [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness). It retains the upstream MIT license and third-party notices. This repository currently contains the upstream source plus this fork plan; the application has not yet been rebranded or released from this fork.

## Roadmap

| ID | Work | Status | Acceptance |
| --- | --- | --- | --- |
| OS-01 | Maintain upstream synchronization | Planned; remotes configured | Record each imported upstream SHA, review the incoming diff, merge into the product branch, resolve conflicts, and run checks appropriate to the affected code before release. No unattended merge or deployment. |
| OS-02 | Audit security and outbound data | Planned | Inventory network destinations and payload producers across the runtime, desktop app, plugins, updates, credentials, analytics, session logs and dependencies. Verify traffic from a source-built application using synthetic data. Separate intentional model requests from developer reporting; document findings and remaining gaps. |
| OS-03 | Workspace folders, instructions and prompts in the application | Planned | The workspace settings show its working directory and additional context folders, access mode, assigned role, instruction sources, precedence and effective prompt. Users can edit writable source instructions and role prompts, preview the result, save or cancel, and see when changes apply. New chats inherit the saved workspace role; restart preserves it. Changes do not silently broaden access or overwrite external file edits. |
| OS-04 | Contribution to upstream | Candidate after OS-03 | Prepare the generic workspace-settings feature on a separate branch based on upstream/master, with focused tests and documentation. Exclude MDDT branding, private context, provider accounts and personal configuration. Opening the upstream PR is a separate step after the feature is implemented and reviewed. |

OS-03 includes visible distinctions between source files, generated snapshots and read-only sources; editing the effective preview alone must not create an undisclosed second source of truth. A changed folder or permission requires the normal access controls. Show concurrent source changes and require reconciliation rather than overwriting them.

## Upstream synchronization

`origin` is the MDDT fork; `upstream` is the original DeepSeek repository. Keep `master` aligned with upstream and maintain product changes on `codex/mddt-agent-os`. Before a planned release or compatibility change, fetch upstream, inspect new commits and session/configuration migrations, and integrate a reviewed revision through a temporary sync branch. Merge-forward preserves published history; do not routinely force-push or rewrite released session data. Record conflicts, imported revision, validation and rollback information in the release notes.

This maintenance workflow is called **upstream synchronization** or **upstream tracking**, not streaming. No scheduled synchronization job has been enabled. Security-relevant upstream fixes receive priority over feature additions.

## Development scope

Prefer scoped plugins and UI/API additions over rewriting the agent loop. Preserve the original repository's development instructions. Review dependency installation scripts and build inputs before running them; a successful code review alone does not establish the safety of a downloaded binary. Keep credentials, private memory and owner-specific configuration outside the tracked repository.
