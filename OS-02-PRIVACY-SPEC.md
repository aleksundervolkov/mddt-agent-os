# OS-02 — default outbound-data controls

2026-10-12. Scope: source defaults in this fork; the installed application and live user configuration are excluded.

## Goal

Keep ordinary requests to the model provider explicitly selected by the user. Do not send additional canonical Session history, product analytics, feedback history, plugin package inventory or stable owner/session identifiers to the Harness developer by default. An explicit override remains possible in the underlying plugins, but no new export UI or consent is claimed.

## Acceptance

1. The base-backed profiles and standalone `sdk-minimal` disable the DeepSeek Session-log and plugin-inventory request extensions by default. A model request after a model switch that sends only current input omits those extensions and synthetic old-history canaries while preserving its ordinary current model input. Test: parsed profile defaults plus request-extension integration with canaries; a real compaction-path egress check remains part of source-build traffic qualification.
2. Feedback stays local by default: recording synthetic feedback does not initialize an OTLP exporter or upload earlier history. Explicit `FEEDBACK_ONLY` still works in tests. Test: real plugin composition with a local collector and negative/positive assertions.
3. Desktop product analytics starts off, never reads identity or emits a product event while off; explicit opt-in remains testable. Test: Desktop bundle/Host analytics composition with local collector.
4. Ordinary DeepSeek model requests omit the stable Harness user ID and session ID by default; explicit opt-in can restore them if needed. Provider authentication, app attribution and required protocol headers remain, and request content is not silently changed. Test: adapter HTTP capture with synthetic IDs in both modes.
5. Documentation states the default export policy, what still reaches the chosen model endpoint, override risks and known limits. Tests and types relevant to changed contracts pass.

## Open questions

1. Process-level read and credential isolation, dependency advisories, updater identity/feed and independently verified source-build network capture require separate work before using confidential workloads or claiming complete isolation.
2. Existing profile/home/CLI patch overlays can override shipped defaults; no audited migration of existing user profiles or installed applications is part of this source-only task.

**Human review:** Security and external-data policy: inspect the egress test evidence and confirm the remaining provider-request and override disclosures before any confidential-workload release.
