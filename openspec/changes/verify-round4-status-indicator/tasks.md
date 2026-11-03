# Tasks

## 1. 共享离线状态语义

- [ ] 1.1 在 `web-design` 增加 `offline` 公共契约和组件映射的失败测试
  **Blocked by:** none
  **Acceptance:** Vitest 通过公开 interface 挂载组件；新测试因 `StatusTone` 和 `StatusBadge` 尚不支持 `offline` 而失败，失败输出被保存为 red evidence
  **Requirements:** prototype-connectivity-status#shared-offline-status
- [ ] 1.2 为 `StatusTone` 和 `StatusBadge` 实现 `offline`
  **Blocked by:** 1.1
  **Acceptance:** 公共类型接受 `offline`，Vitest、typecheck 和 build 通过，渲染结果同时包含中性状态 class、状态点与插槽文字
  **Requirements:** prototype-connectivity-status#shared-offline-status

## 2. 前端消费

- [ ] 2.1 在 `web-front` 增加顶栏共享状态组件的失败测试
  **Blocked by:** 1.2
  **Acceptance:** Vitest 挂载页面；新测试因顶栏仍使用普通文本标签而失败，且断言目标包含 `offline` tone 和“静态原型 · 未连接 Agent”文案，失败输出被保存为 red evidence
  **Requirements:** prototype-connectivity-status#topbar-disconnected-status
- [ ] 2.2 用 `StatusBadge tone="offline"` 替换顶栏本地标签并移除失去用途的样式
  **Blocked by:** 2.1
  **Acceptance:** 顶栏通过共享组件显示“静态原型 · 未连接 Agent”，页面没有复制状态样式，消费仓的 Vitest、typecheck 和 build 通过
  **Requirements:** prototype-connectivity-status#topbar-disconnected-status
