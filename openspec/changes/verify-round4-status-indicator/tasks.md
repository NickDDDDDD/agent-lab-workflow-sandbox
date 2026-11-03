# Tasks

## 1. 共享离线状态语义

- [ ] 1.1 在 `web-design` 增加 `offline` 公共契约和组件映射的失败测试
  **Acceptance:** 新测试因 `StatusTone` 和 `StatusBadge` 尚不支持 `offline` 而失败，现有检查仍保持原结果
  **Requirements:** prototype-connectivity-status#shared-offline-status
- [ ] 1.2 为 `StatusTone` 和 `StatusBadge` 实现 `offline`
  **Acceptance:** 公共类型接受 `offline`，组件测试、typecheck 和 build 通过，渲染结果同时包含离线视觉提示与插槽文字
  **Requirements:** prototype-connectivity-status#shared-offline-status

## 2. 前端消费

- [ ] 2.1 在 `web-front` 增加顶栏共享状态组件的失败测试
  **Acceptance:** 新测试因顶栏仍使用普通文本标签而失败，且断言目标包含 `offline` tone 和“未连接 Agent”文案
  **Requirements:** prototype-connectivity-status#topbar-disconnected-status
- [ ] 2.2 用 `StatusBadge tone="offline"` 替换顶栏本地标签并移除失去用途的样式
  **Acceptance:** 顶栏通过共享组件显示“未连接 Agent”，页面没有复制状态样式，更新后的本地组件包可由消费仓完成测试、typecheck 和 build
  **Requirements:** prototype-connectivity-status#topbar-disconnected-status
