# prototype-connectivity-status Delta

## Purpose

为静态协作原型提供跨仓一致、可访问且可自动验证的连接状态表达，使设计系统与消费页面共享同一离线语义，同时不暗示已经接入真实 Agent。

## ADDED Requirements

### Requirement: 设计系统提供共享离线状态

`web-design` MUST 通过公开的 `StatusTone` 和 `StatusBadge` 支持 `offline` 状态。离线状态 MUST 具有区别于 active、waiting、idle、done 的中性视觉提示，并 MUST 与可见文字共同传达语义，不得只依赖颜色。

#### Scenario: 消费方渲染离线状态

- **WHEN** 消费方以 `tone="offline"` 渲染 `StatusBadge` 并提供状态文字
- **THEN** TypeScript 接受该公共类型，组件显示离线视觉提示和消费方提供的文字

### Requirement: 顶栏清晰展示未连接状态

`web-front` MUST 在顶栏通过 `web-design` 的共享 `StatusBadge` 展示“未连接 Agent”，并 MUST 保持该状态属于静态原型说明。页面 MUST NOT 复制 `StatusBadge` 的状态颜色、圆点或文字排版规则。

#### Scenario: 用户查看静态原型顶栏

- **WHEN** 用户打开调度总览页面
- **THEN** 顶栏显示由共享组件渲染的“未连接 Agent”状态，且不会暗示页面已连接真实 Agent

#### Scenario: 页面在窄视口换行

- **WHEN** 顶栏因可用宽度不足而换行
- **THEN** 未连接状态文字仍完整可见，且不与面包屑内容重叠

