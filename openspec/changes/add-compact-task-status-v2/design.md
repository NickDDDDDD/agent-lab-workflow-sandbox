# Design

## Context

见 `proposal.md` 的 Why。当前 `web-design` 的 StatusBadge 只有 `tone` 属性并使用固定 Tailwind 尺寸；`web-plugin` 的 TaskQueue 直接渲染该组件；`web-front` 只有一个 TaskQueue 装配点。三个仓通过本地包依赖形成 design → plugin → front 的单向链路。

## Goals / Non-Goals

**Goals:**

- 以向后兼容的公共属性表达密度，而不是让消费者覆盖内部样式。
- 让 TaskQueue 负责把队列级选择一致地传给全部状态徽标。
- 保持状态文本、色调、圆点和无障碍语义不变。

**Non-Goals:**

- 不修改任务状态枚举、任务数据结构或 AgentRoster。
- 不引入全局密度主题、响应式自动切换或新依赖。
- 不重新设计徽标颜色、圆角或任务队列布局。

## Decisions

### 1. 使用加法式布尔属性表达紧凑密度

StatusBadge 增加默认关闭的 `compact` 属性；组件内部选择密度类。相比让消费者传入任意 class，这一方式保留设计系统对间距和字号的所有权，并保持未修改消费者的输出兼容。

### 2. TaskQueue 使用队列级属性

TaskQueue 增加默认关闭的 `compactStatus` 属性，并把它传给每个 StatusBadge。相比在 Task 数据中增加展示字段，队列级属性不会污染领域数据，也保证同一队列内表现一致。

### 3. 由 Web Front 显式启用

Web Front 在唯一 TaskQueue 装配点启用紧凑模式。AgentRoster 不接收任何新配置，因此继续使用默认密度。

### 4. 按依赖方向验证

实现和验证顺序为 web-design → web-plugin → web-front。每个仓先用 TypeScript/Vue 编译合同暴露缺失接口，再实现最小改动并运行该仓 typecheck/build；最终运行 Workspace verify Profile。

## Risks / Trade-offs

- [紧凑字号可能降低可读性] → 只做一级密度收缩并保留完整文本、色调和圆点，不隐藏内容。
- [本地 file 依赖可能使用旧构建产物] → 按依赖顺序重新构建，并在下游验证前刷新本地安装。
- [布尔属性未来不足以表达更多密度] → 当前只有两个明确模式；出现第三种需求时再演进为受限枚举，避免提前设计。

## Migration Plan

这是向后兼容的加法式接口。先发布 web-design，再发布 web-plugin，最后更新 web-front；回滚时逆序撤销消费者启用和两个可选属性。
