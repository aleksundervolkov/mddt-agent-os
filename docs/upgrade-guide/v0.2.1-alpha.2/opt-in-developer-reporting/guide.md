---
kind: upgrade-guide
description: "Session-log, feedback telemetry, product analytics, plugin inventory and provider identity now default to local-only behavior."
---

# Developer reporting is opt-in

English | [中文](guide.zh.md)

## Change

Shipped profiles previously uploaded canonical Session history with DeepSeek requests, sent plugin package inventory, exported Session history after feedback, and collected Desktop product analytics by default. DeepSeek requests also carried a persistent installation id and optional Session id. These extras are now disabled by default; ordinary requests still reach the selected model provider, with application attribution in `User-Agent`. Existing profile, home and invocation patches can override the new defaults; neither installed applications nor saved user configurations are migrated.

## Migration

1. Review `session-log-deepseek.enabled`, `plugin-package-inventory-deepseek.enabled`, `session-telemetry-otel.mode`, and DeepSeek provider `sendInstallationIdentity` in profile/home patches and saved settings. Review Desktop Cordis configuration for `product-analytics.enabled`; it has no user-facing control. Also inspect `DSH_TELEMETRY_MODE`: an inherited `FEEDBACK_ONLY` value overrides the disabled bundle default, so unset it or set `DISABLED`. Set enabled fields to `false` and telemetry mode to `DISABLED` wherever higher-precedence configuration persists; removing a patch entry does not clear saved settings. Use explicit opt-in only after reviewing the payload and its destination; `FEEDBACK_ONLY` exports the canonical history prefix, not just feedback text.
2. Check the resolved profile configuration and confirm the fields are disabled before handling confidential data. Validate actual outbound traffic from a source-built application with synthetic canaries; source defaults alone do not establish process read isolation or a cleared update feed.
