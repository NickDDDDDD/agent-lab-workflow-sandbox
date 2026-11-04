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

在 `StatusTone` 中加入 `offline`，并在 `StatusBadge` 的穷举映射中提供中性的离线视觉。连接状态仍由可见文字说明，颜色只作为辅助提示。这个 interface 只增加一个合法状态值，却让所有消费方复用组件内的视觉、状态点和排版，保持 module 的深度和样式 locality。

备选方案是新增 `ConnectionStatus`，但它只会把布尔连接状态透传给 `StatusBadge`，形成没有额外行为的浅 module；另一个方案是复用 `idle`，但会混淆“已连接但空闲”和“未连接”两种可观察语义。

### 2. web-front 只负责选择状态和文案

顶栏直接导入并使用 `StatusBadge`，传入 `offline` 和“静态原型 · 未连接 Agent”文案。状态视觉归 `web-design`，页面布局和原型说明归 `web-front`，不复制共享 module 的实现样式。

备选方案是在 `web-front` 保留 `.prototype-label` 并只调整文字，但这会继续让同一状态跨越两个样式 seam，后续修正需要修改多个调用方。

### 3. 用窄范围自动化验证共享契约与消费结果

两个仓都复用现有 Vite 工具链，增加 Vitest、Vue Test Utils 和轻量 DOM 环境。每个仓对应一个纵向 Build package，由同一个 package 完整拥有 red、green 和 regression evidence，避免把失败测试与实现拆成无法独立完成 TDD 契约的任务。`web-design` 通过公开 interface 挂载 `StatusBadge`，验证 `offline` 的文字、状态点和中性 class；`web-front` 挂载 `App`，验证顶栏渲染共享状态 module 和完整原型文案。各仓仍执行 typecheck/build，确认声明产物和跨仓消费未破坏。

备选方案是用文本搜索断言源码，虽然依赖少，但它只验证实现字符串，无法证明 Vue 渲染或公共类型可用；仅依赖 build 也无法形成先失败后通过的行为级 TDD 证据。

## Risks / Trade-offs

- [公共 union 类型扩展可能影响穷举消费者] → 在设计仓执行类型检查，并在消费仓重新安装本地包后执行 typecheck/build。
- [静态离线标识可能被误解为实时探测] → 保留“静态原型”上下文，并明确显示“未连接 Agent”。
- [两仓提交短暂不同步] → 先发布 `web-design` 分支提交，再让 `web-front` 消费同一轮本地包；任一仓失败时不把 Change 推进到 Verify。

## Migration Plan

先扩展 `web-design` 公共类型和组件映射，再更新 `web-front` 消费点。回退时先恢复消费页面，再移除 `offline` 公共 API，避免页面引用不存在的类型成员。
