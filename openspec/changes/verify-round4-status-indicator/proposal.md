# Proposal

## Why

当前 `web-front` 顶栏用普通文本标记“静态原型 · 未连接 Agent”，而 `web-design` 的 `StatusBadge` 缺少明确表达“离线/未连接”的共享语义。这个小型双仓改动可在不接入真实后端的前提下统一状态表达，并验证 Repoctopus 的跨仓工作流。

## What Changes

- `web-design` 为 `StatusBadge` 增加公开的 `offline` tone，并保持文字与状态点共同传达状态。
- `web-front` 在顶栏使用共享 `StatusBadge` 展示“未连接 Agent”，替换当前普通文本标签。
- 为共享类型、组件表现和消费页面补充自动化验证。

## Capabilities

### New Capabilities

- `prototype-connectivity-status`: 设计系统提供离线状态语义，消费页面以统一组件清晰展示原型未连接状态。

### Modified Capabilities

无。

## Impact

- 影响 `web-design` 的公开 `StatusTone` 类型和 `StatusBadge` 样式映射。
- 影响 `web-front` 顶栏组件消费和对应自动化测试。
- 不新增运行时依赖，不改变 `web-plugin`、`backend` 或真实连接协议。
