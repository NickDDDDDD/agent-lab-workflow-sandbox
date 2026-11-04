# Tasks

## 1. 共享离线状态语义

- [ ] 1.1 在 `web-design` 以完整 TDD 闭环交付 `offline` 公共契约和组件映射
  **Blocked by:** none
  **Acceptance:** 先通过公开 interface 挂载组件并保存因 `StatusTone` 和 `StatusBadge` 尚不支持 `offline` 而产生的 Vitest red evidence；随后实现公共类型与中性状态映射，并保存 green evidence；最后 Vitest 回归、typecheck 和 build 全部通过，渲染结果同时包含中性状态 class、状态点与插槽文字
  **Requirements:** prototype-connectivity-status#shared-offline-status

## 2. 前端消费

- [ ] 2.1 在 `web-front` 以完整 TDD 闭环改用共享离线状态组件
  **Blocked by:** 1.1
  **Acceptance:** 先挂载页面并保存因顶栏仍使用普通文本标签而产生的 Vitest red evidence，断言目标包含 `offline` tone 和“静态原型 · 未连接 Agent”文案；随后用 `StatusBadge tone="offline"` 替换本地标签并移除失去用途的样式，保存 green evidence；最后 Vitest 回归、typecheck 和 build 全部通过，页面没有复制共享状态样式
  **Requirements:** prototype-connectivity-status#topbar-disconnected-status
