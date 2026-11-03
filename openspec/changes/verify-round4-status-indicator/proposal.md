# Proposal

## Why

当前 `web-front` 顶栏用普通文本标记“静态原型 · 未连接 Agent”，而 `web-design` 的 `StatusBadge` 只提供 active、waiting、idle、done 四种状态，缺少明确表达“离线/未连接”的共享语义。这个小型双仓改动可以在不接入真实后端的前提下，让原型边界更清晰，并用于验证 Repoctopus 的跨仓 Open、Design、Build、Verify、Archive 流程。

## What Changes

- `web-design` 为 `StatusBadge` 增加公开的 `offline` tone，并保持文字与状态点共同传达状态。
- `web-front` 在顶栏使用共享 `StatusBadge` 展示“未连接 Agent”，替换当前普通文本标签。
- 为共享类型、组件表现和消费页面补充自动化验证。

## Capabilities

### Added Capabilities

- `prototype-connectivity-status`: 设计系统提供离线状态语义，消费页面以统一组件清晰展示原型未连接状态。

## Dependencies

本 Change 复用 `web-design` 现有 `StatusBadge` 与 `web-front` 现有顶栏，不新增运行时依赖，也不改变 `web-plugin` 或 `backend` 的接口。

## 非目标

- 不接入真实 Agent、轮询、WebSocket 或后端健康检查。
- 不改变任务、Agent 或运行记录的静态演示数据。
- 不扩展除 `offline` 以外的状态模型。
