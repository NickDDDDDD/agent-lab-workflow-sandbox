# Design

## Context

`web-design/src/StatusBadge.vue` 通过 `StatusTone` 到 Tailwind class 的穷举映射提供状态样式；`web-front/src/App.vue` 已消费同一组件包，但顶栏的连接状态仍由本地 `.prototype-label` 文本实现。两者形成了重复的状态表达，且 `idle` 不能准确区分“空闲”和“尚未连接”。

## Goals / Non-Goals

**Goals:**

- 在现有公共组件中建立明确、可测试的离线状态语义。
- 让页面只选择状态和文案，不复制设计系统内部样式。

**Non-Goals:**

- 不建立真实连接状态源或连接状态机。
- 不改变静态 Agent、任务和运行记录数据。

## Decisions

### 1. 扩展现有 StatusBadge，而不是新增连接专用组件

在 `StatusTone` 中加入 `offline`，并在 `StatusBadge` 的穷举映射中提供中性的离线视觉。连接状态仍由可见文字说明，颜色只作为辅助提示。这样保持 API 小而明确，也避免仅为一个静态原型状态引入新的组件层。

### 2. web-front 只负责选择状态和文案

顶栏直接导入并使用 `StatusBadge`，传入 `offline` 和“未连接 Agent”文案。样式语义归 `web-design`，页面布局和原型说明归 `web-front`，不复制共享组件内部样式。

### 3. 用窄范围自动化验证共享契约与消费结果

`web-design` 验证 `offline` 类型和渲染样式映射；`web-front` 验证顶栏渲染共享组件及明确文案。各仓仍执行现有 typecheck/build，确认包导出和跨仓消费未破坏。

## Risks / Trade-offs

- [公共 union 类型扩展可能影响穷举消费者] → 在设计仓执行类型检查，并在消费仓重新安装本地包后执行 typecheck/build。
- [静态离线标识可能被误解为实时探测] → 保留“静态原型”上下文，并明确显示“未连接 Agent”。
- [两仓提交短暂不同步] → 先发布 `web-design` 分支提交，再让 `web-front` 消费同一轮本地包；任一仓失败时不把 Change 推进到 Verify。

## Migration Plan

先扩展 `web-design` 公共类型和组件映射，再更新 `web-front` 消费点。回退时先恢复消费页面，再移除 `offline` 公共 API，避免页面引用不存在的类型成员。
