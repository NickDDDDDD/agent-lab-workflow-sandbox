# Tasks

## 1. 共享离线状态语义

- [ ] 1.1 在 `web-design` 先增加失败测试，证明 `StatusTone` 和 `StatusBadge` 尚不支持 `offline`；Acceptance: 测试因缺少公共类型或样式映射而失败；Trace: `prototype-connectivity-status` 的“共享离线状态”要求。
- [ ] 1.2 为 `StatusTone`、`StatusBadge` 实现 `offline`，并运行组件测试、typecheck 和 build；Acceptance: 公共类型可消费，组件同时渲染离线视觉提示与插槽文字；Trace: `prototype-connectivity-status` 的“共享离线状态”要求。

## 2. 前端消费

- [ ] 2.1 在 `web-front` 先增加失败测试，证明顶栏尚未通过共享组件展示“未连接 Agent”；Acceptance: 测试因当前普通文本标签而失败；Trace: `prototype-connectivity-status` 的“顶栏连接状态”要求。
- [ ] 2.2 用 `StatusBadge tone="offline"` 替换顶栏本地标签并移除失去用途的样式；Acceptance: 顶栏显示明确的“未连接 Agent”文字，页面不复制共享状态样式，更新后的本地组件包可由消费仓完成 typecheck 和 build；Trace: `prototype-connectivity-status` 的“顶栏连接状态”要求。
