# 组件查询工作流

当用户询问"X 组件怎么用"或"怎么实现 Y 功能"时，按以下步骤执行。

## 步骤

### 1. 判断路由方式

| 用户输入特征 | 路由方式 | 下一步 |
|-------------|---------|--------|
| 明确说了组件名（如"DataTable"） | 关键词路由 | 查 `../quickref/keyword-router.md` 定位文档 |
| 描述了需求（如"我要做一个搜索表格"） | 需求路由 | 查 `../quickref/component-router.md` 匹配组件 |
| 问两个组件的区别（如"Table 和 DataTable 用哪个"） | 选型决策 | 查 `../rules/selection-rules.md` |

### 2. 分层读取文档

```
第一层: quickref/ 速查表（覆盖 80% 常见问题）
  ↓ 不够
第二层: references/ 对应组件 readme.md、api.md 或 layouts/*.md
  ↓ 不够
第三层: references/ 对应组件 demos/
  ↓ 不够或有矛盾
第四层: node_modules/ 源码（Base → @tinper/next-ui, Pro → tne-tinpernextpro-fe）
```

### 3. 检查踩坑指南

回答前扫描 `../gotchas/` 目录，确认答案不涉及已知坑：
- `../gotchas/react18-compat.md` — React 18 兼容问题
- `../gotchas/api-differences.md` — 与 antd 的 API 差异
- `../gotchas/pro-install.md` — Pro 包安装问题
- `../gotchas/known-issues.md` — 其他已知问题

### 4. 补充组合模式

如果用户的需求涉及多组件组合，补充 `../patterns/` 中的相关模式作为参考：
- `../patterns/page-patterns.md` — 页面结构模式
- `../patterns/modal-patterns.md` — 弹窗组合模式
- `../patterns/table-patterns.md` — 表格使用模式
- `../patterns/form-patterns.md` — 表单使用模式
- `../patterns/layout-patterns.md` — 布局模式

### 5. 回答规范

- 必须先读文档再回答，禁止凭记忆编造
- 使用 `visible` 不使用 `show`
- 提及安装时必须注明 ynpm
- 如果涉及已知坑，主动提醒用户
