# Design

## Context

`web-design/src/StatusBadge.vue` 通过 `StatusTone` 到 Tailwind class 的穷举映射提供状态样式；`web-front/src/App.vue` 已消费同一组件包，但顶栏的连接状态仍由本地 `.prototype-label` 文本实现。两者形成了重复的状态表达，且 `idle` 不能准确区分“空闲”和“尚未连接”。

## Decisions

### 1. 扩展现有 StatusBadge，而不是新增连接专用组件

在 `StatusTone` 中加入 `offline`，并在 `StatusBadge` 的穷举映射中提供中性的离线视觉。连接状态仍由可见文字说明，颜色只作为辅助提示。这样保持 API 小而明确，也避免仅为一个静态原型状态引入新的组件层。

### 2. web-front 只负责选择状态和文案

顶栏直接导入并使用 `StatusBadge`，传入 `offline` 和“未连接 Agent”文案。样式语义归 `web-design`，页面布局和原型说明归 `web-front`，不复制共享组件内部样式。

### 3. 用窄范围自动化验证共享契约与消费结果

`web-design` 验证 `offline` 类型和渲染样式映射；`web-front` 验证顶栏渲染共享组件及明确文案。各仓仍执行现有 typecheck/build，确认包导出和跨仓消费未破坏。

## Recovery and Failure

如果组件包未重新打包或消费仓未获得更新后的类型，`web-front` typecheck/build 必须失败而不是退回本地字符串样式。回退时同时移除消费点和 `offline` 公共 API，避免两仓契约不一致。

## Stop Conditions

- 实现需要新增真实连接状态源或修改后端协议；
- `offline` 无法通过共享包的公开类型被消费；
- 验证只能依赖人工视觉检查，无法覆盖公共 API 与页面输出。
