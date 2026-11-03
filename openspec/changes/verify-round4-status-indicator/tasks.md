# Tasks

## 1. 共享离线状态语义

- [ ] 1.1 在 `web-design` 先增加失败测试，证明 `StatusTone` 和 `StatusBadge` 尚不支持 `offline`；Acceptance: 测试因缺少公共类型或样式映射而失败；Trace: `prototype-connectivity-status` 的“共享离线状态”要求。
- [ ] 1.2 为 `StatusTone`、`StatusBadge` 实现 `offline`，并运行组件测试、typecheck 和 build；Acceptance: 公共类型可消费，组件同时渲染离线视觉提示与插槽文字；Trace: `prototype-connectivity-status` 的“共享离线状态”要求。

## 2. 前端消费

- [ ] 2.1 在 `web-front` 先增加失败测试，证明顶栏尚未通过共享组件展示“未连接 Agent”；Acceptance: 测试因当前普通文本标签而失败；Trace: `prototype-connectivity-status` 的“顶栏连接状态”要求。
- [ ] 2.2 用 `StatusBadge tone="offline"` 替换顶栏本地标签并移除失去用途的样式；Acceptance: 顶栏显示明确的“未连接 Agent”文字，页面不复制共享状态样式；Trace: `prototype-connectivity-status` 的“顶栏连接状态”要求。

## 3. 跨仓验证

- [ ] 3.1 按项目依赖顺序重新打包 `web-design` 并验证 `web-front`；Acceptance: 两仓 typecheck/build 和相关测试通过，`backend` 与 `web-plugin` 无实现改动；Trace: 全部 Change requirements。
- [ ] 3.2 执行工作空间 required checks 并记录验证证据；Acceptance: Runtime 派发的检查全部成功，规格、实现和证据可追溯；Trace: 全部 Change requirements。
