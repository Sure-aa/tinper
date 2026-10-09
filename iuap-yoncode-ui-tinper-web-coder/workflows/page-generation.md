# 页面生成工作流

当任务是"根据设计图生成页面"或"重构现有页面"时，按以下步骤执行。

## 步骤

### 1. 识别页面类型

| 页面类型 | 典型特征 | 参考模式 |
|---------|---------|---------|
| 列表页 | 搜索条件 + 数据表格 + 操作按钮 | `../patterns/page-patterns.md` 模式1 + `../patterns/table-patterns.md` |
| 编辑弹窗 | Modal + 表单 | `../patterns/modal-patterns.md` 第3节 |
| 详情页 | Tabs + 折叠面板 + 只读表单 | `../patterns/page-patterns.md` 模式5+6 |
| 向导页 | Steps + 多步表单 | `../patterns/page-patterns.md` 模式9 |

### 2. 选型决策

1. 查阅 `../rules/selection-rules.md` 确定每个区域用什么组件
2. 企业场景优先 Pro 组件（DataForm > Form, SearchForm > Form）
3. **表格区先判断「改动已有表格」还是「新建表格」**（`../rules/selection-rules.md` 决策 0）：
   - 改动项目已有表格：保持原组件类型，不要替换为 Grid 系列
   - 新建表格：优先 Grid 系列 —— 可编辑/子表/明细/增删行用 **EditGrid**，基础/普通表格用 **TinperGrid**，其余用 **DataGrid**；仅用户明确指定才用 DataTable/EditTable/Table
4. 同页面保持 Pro/Base 一致性，且避免同页混用两套表格体系

### 3. 组件组合

1. 查阅 `../patterns/` 对应模式文件，获取组合代码参考
2. 所有工具栏用 Space 包裹
3. 弹窗表单必加 `maskClosable={false}`（默认已是 false，显式写增强可读性）

### 4. 样式落地

1. 读取 `../DESIGN.md` 和 `../designtoken.css`
2. 优先复用 `--ynfw-*` / `--wui-*` / `--brand-*` 语义 token
3. 禁止新建与品牌语义重复的颜色 token

### 5. 校验清单

- [ ] 所有组件从 `@tinper/next-ui` 或 `tne-tinpernextpro-fe` 导入
- [ ] 没有裸 div 替代可用组件的情况
- [ ] Modal/Drawer 使用 `visible` 而非 `show`
- [ ] Modal 使用 `maskClosable` 而非废弃的 `backdropClosable`
- [ ] Table/DataTable 数据有唯一 key
- [ ] DatePicker 传 Moment 对象
- [ ] 无 `Typography.Title` / `Typography.Text` 使用
- [ ] 说明哪些区域用了组件、哪些没用及原因
