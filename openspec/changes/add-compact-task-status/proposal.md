# Proposal

## Why

任务队列同时展示标识、标题、仓库、Agent 与状态，现有舒展型状态徽标会放大每一行的视觉重量。需要一个显式、可复用且不改变状态语义的紧凑密度，让高信息密度区域保持清晰。

## What Changes

- 为状态徽标增加可选的紧凑密度，默认外观保持不变。
- 允许任务队列选择紧凑状态徽标，并保持其他消费者不受影响。
- 在调度台任务队列启用紧凑状态展示。

## Capabilities

### New Capabilities

- `task-status-presentation`: 定义状态徽标的密度选择、任务队列的传递行为以及调度台的紧凑展示。

### Modified Capabilities

无。

## Impact

- `web-design` 的 StatusBadge 公共组件接口和样式。
- `web-plugin` 的 TaskQueue 公共组件接口。
- `web-front` 的任务队列装配。
- 不增加运行时依赖，不改变任务数据结构或状态枚举。
