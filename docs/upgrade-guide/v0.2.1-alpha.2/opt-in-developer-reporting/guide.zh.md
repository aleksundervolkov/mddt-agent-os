---
kind: upgrade-guide
description: "会话日志、反馈遥测、产品分析、插件清单与提供方身份现在默认仅留在本地。"
---

# 开发者报告需明确启用

[English](guide.md) | 中文

## 变更

随附 profile 之前默认随 DeepSeek 请求上传权威会话历史、发送插件包清单、在反馈后导出会话历史，并收集桌面端产品分析。DeepSeek 请求还携带持久安装 id 和可选的 Session id。现在这些附加通道默认关闭；普通请求仍会发送到选定的模型提供方，并在 `User-Agent` 中携带应用归因。现有 profile、home 和调用时 patch 仍可覆盖新默认值；已安装应用与保存的用户配置不会被迁移。

## 迁移

1. 检查 profile/home patch 和保存的设置中的 `session-log-deepseek.enabled`、`plugin-package-inventory-deepseek.enabled`、`session-telemetry-otel.mode` 以及 DeepSeek 提供方的 `sendInstallationIdentity`。检查桌面端 Cordis 配置中的 `product-analytics.enabled`；它没有面向用户的开关。还应检查 `DSH_TELEMETRY_MODE`：继承的 `FEEDBACK_ONLY` 会覆盖 bundle 的禁用默认值，应取消该变量或设为 `DISABLED`。在仍生效的高优先级配置中，将 enabled 字段明确设为 `false`，遥测 mode 设为 `DISABLED`；删除 patch 条目不会清除保存的设置。只有审查载荷及目的地后才明确启用；`FEEDBACK_ONLY` 导出权威历史前缀，不只是反馈文字。
2. 检查解析后的 profile 配置，确认这些字段在处理机密数据前处于禁用状态。使用合成标记验证从源代码构建的应用的实际出站流量；仅凭源代码默认值不能证明进程读取隔离或更新源已经清理。
