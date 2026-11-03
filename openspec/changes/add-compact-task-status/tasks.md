# Tasks

## 1. 状态徽标密度合同

- [ ] 1.1 先增加紧凑属性的编译合同并确认旧组件接口不能通过，再为 StatusBadge 实现默认/紧凑密度；运行 `npm run typecheck` 与 `npm run build`。
      **Acceptance:** 默认调用保持现有密度；显式 `compact` 调用通过编译并产生更小的间距、内边距和视觉占用；文本、色调和状态圆点不变。
      **Requirements:** task-status-presentation / 状态徽标支持显式密度

## 2. 任务队列传递

- [ ] 2.1 先增加 TaskQueue 紧凑状态属性的编译合同并确认旧接口不能通过，再把队列级选择传给每个 StatusBadge；运行 `npm run typecheck` 与 `npm run build`。
      **Acceptance:** `compactStatus` 为真时全部任务徽标接收紧凑密度；省略该属性时保持默认密度。
      **Requirements:** task-status-presentation / 任务队列传递密度选择

## 3. 调度台装配

- [ ] 3.1 在 Web Front 的任务队列装配点启用紧凑状态，保持 AgentRoster 不变；运行 `npm run build`。
      **Acceptance:** TaskQueue 显式启用紧凑状态；AgentRoster 没有密度配置变化；完整前端构建通过。
      **Requirements:** task-status-presentation / 调度台任务队列使用紧凑状态

## 4. 跨仓验收

- [ ] 4.1 按 Workspace verify Profile 运行 design typecheck/build、plugin typecheck/build、front build、backend verify 与协调仓完整性检查。
      **Acceptance:** Runtime 提供的全部验证命令退出码为零，三个实现仓的 source branch 与 checkpoint 可追溯且没有未授权仓变化。
      **Requirements:** task-status-presentation / 状态徽标支持显式密度; task-status-presentation / 任务队列传递密度选择; task-status-presentation / 调度台任务队列使用紧凑状态
