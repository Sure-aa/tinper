# 选型决策表（"X 和 Y 用哪个？"）

同一需求有多种组件可选时，必须先查阅本表再推荐。

---

## 决策 0: 表格组件选择算法（最高优先级，遇到任何表格需求先走这一步）

**核心判断轴：当前需求是「改动项目已有表格」还是「新建一张表格」。** 不要再用"新项目/旧项目"做判断。按以下顺序逐条判断：

1. **用户是否明确指定了组件？**
   - 指定 `DataGrid` / `EditGrid` / `TinperGrid`：按用户指定。
   - 指定 `@tinper/next-ui Table` / `DataTable` / `EditTable`：按用户指定；若与"新建优先 Grid"的约定冲突，先提醒用户确认再继续。
2. **当前需求是「在项目已有表格的基础上改动」吗？**（增删列、改请求、加操作列、调样式等）
   - 是：**直接在已有表格上改，保持其原组件类型，不要把 `@tinper/next-ui Table` / `DataTable` / `EditTable` 替换为 Grid 系列。**
   - 否（要新建表格）：进入下一步。
3. **新建的是可编辑表格、子表、明细表、行内编辑、增行、删行、单元格校验吗？**
   - 是：优先 **EditGrid**。
   - 否：进入下一步。
4. **用户是否明确说明需要基础/普通表格、或按需引入 Grid 模块？**（用户主动说了"基础表格""普通表格""按需引入"等关键词）
   - 是：优先 **TinperGrid**。
   - 否：优先 **DataGrid**（列表页、大数据、冻结列、拖拽列、业务表格、以及其他未明确指定类型的新建表格）。
5. **仅当用户明确要求**使用 `@tinper/next-ui Table` / `DataTable` / `EditTable` / `wui-table` 时，才使用它们。
6. **TinperGrid 与 DataGrid 难以区分时，优先 DataGrid。**

> **同页一致性边界**：新建表格但同页已有 Table/DataTable/EditTable 体系时，以"不替换已有 + 新表与同页保持一致"为准，避免同页混用两套表格体系（与核心指令 15 一致）。

---

## 决策 1: Table vs DataTable vs EditTable vs DataGrid vs EditGrid vs TinperGrid

> 先走「决策 0 选择算法」确定改动还是新建。下表给出**新建表格**时的首选/备选；改动已有表格时一律保持原组件不替换。

| 业务场景（新建表格） | 首选组件 | 备选组件 | 说明 |
| --- | --- | --- | --- |
| 行内编辑、子表、明细表、增删行、单元格校验 | **EditGrid** | EditTable | 仅用户明确要求时才用 EditTable |
| 列表页 + 分页请求 + 操作列 + 行选择 + 排序筛选 | **DataGrid** | DataTable | 仅用户明确要求时才用 DataTable |
| 大数据 / 冻结列 / 拖拽列 / 复杂业务表格 | **DataGrid** | DataTable / Table+HOCs | 优先 Grid 系列 |
| 基础/普通表格、按需引入表格功能模块 | **TinperGrid** | wui-table | 不默认使用 @tinper/next-ui Table，仅用户明确要求时才用 @tinper/next-ui Table |
| 表格卡片/列表双视图切换 | **DataGrid** | DataTable | DataGrid 用 `displayMode`/`cardConfig`/`kanbanConfig`，DataTable 用 `mode`/`showModeSwitch` |
| 改动已有表格（任意类型） | **保持原组件** | — | 不替换为 Grid 系列，直接在原表上改 |

### 反例约束（防止误选 EditTable / 误替换）

当需求出现以下关键词时，**不要默认选 `EditTable`，也不要把已有表格替换成 Grid**：

`子表`、`明细表`、`行内编辑`、`可编辑表格`、`增行`、`删行`、`批量编辑`、`单元格编辑`、`单元格校验`、`DataGrid`、`EditGrid`、`TinperGrid`

正确处理：先按决策 0 判断是「改动已有」还是「新建」——
- 改动已有：在原表上改，保持原组件，不替换。
- 新建：可编辑场景优先 **EditGrid**，仅用户明确指定才用 EditTable。

### 特例：把旧 wui-table 主动升级到高性能 Grid（GridCompat）

决策 0 的「改动已有表格保持原组件」有一条**主动升级**例外：当用户明确要求「把已有的 `@tinper/next-ui Table` / wui-table 换成高性能虚拟滚动表格」时，可选用 **`GridCompat`（对外导出名 `Table`，来自 `tne-tinpernextpro-fe`）**——它用 `@tinper/grid` 内核渲染、保留 wui-table 的 `columns`/HOC API，是存量低迁移成本的过渡方案。

- 仅用于「旧 wui-table → Grid 性能」的存量迁移；**新建表格仍首选 `DataGrid` / `EditGrid`**，不要把 GridCompat 当新项目主力表格。
- 注意命名辨析：`tne-tinpernextpro-fe` 的 `Table`（GridCompat，Grid 内核）与 `@tinper/next-ui` 的 `Table`（wui-table，DOM 内核）同名但不同物，导入时确认来源包。
- 详见 `../references/GridCompat/readme.md`。

## 决策 2: Form vs DataForm vs SearchForm

| 判断条件 | 选型 | 理由 |
| --- | --- | --- |
| 列表页查询条件区（需折叠/展开/已选条件/内置查询重置） | **SearchForm** | 继承 DataForm + 查询特有能力 |
| 新增/编辑/详情表单（多字段/自适应布局/编辑浏览态切换） | **DataForm** | 22 种 inputType、formMode、hiddenKeys |
| 字段少于 4 个的简单表单、无需自适应布局 | **Form** | 更轻量，直接控制 |
| 表单项高度自定义、inputType 覆盖不到 | **Form + 手写 FormItem** | DataForm 回退方案 |

## 决策 3: Modal 声明式 vs 命令式

| 判断条件 | 选型 | 示例 |
| --- | --- | --- |
| 自定义复杂内容（表单/表格/多步操作） | 声明式 `<Modal visible={} >` | 新增/编辑弹窗 |
| 简单确认/提示 | 命令式 `Modal.confirm()` | 删除确认 |
| 弹窗内容需要组件状态或 ref | 声明式 | 弹窗内有 DataForm |
| 需要弹窗外动态更新内容 | 命令式 + `modal.update()` | 异步流程状态更新 |

## 决策 4: Form API 风格

| 判断条件 | 选型 | 示例 |
| --- | --- | --- |
| 函数组件 | `Form.useForm()` Hook 式 | `const [form] = Form.useForm()` |
| 类组件/旧项目 | `Form.createForm()` HOC 式 | 旧模式，新项目不推荐 |
| Pro 组件（DataForm/SearchForm） | `ref={formRef}` | `formRef.current.validateFields()` |

## 决策 5: Select 相关组件选择

| 判断条件 | 选型 | 关键属性 |
| --- | --- | --- |
| 单选下拉 | Select 默认 | `options` `onChange` |
| 多选下拉 | Select + `mode="multiple"` | `maxTagCount` |
| 可搜索下拉 | Select + `showSearch` | `filterOption` 或 `onSearch` |
| 可输入创建标签 | Select + `mode="tags"` | `tokenSeparators` |
| 表格形式下拉搜索 | InputSelect (Pro) | `columns` `dataSource` `multiple` |
| 树形数据选择 | TreeSelect | `treeData` `showSearch` |
| 级联数据选择 | Cascader | `options` `loadData` |
| 分组级联 | GroupCascader (Pro) | `options` `loadDataFlag` `showSearch` |

## 决策 6: 反馈提示分层

| 判断条件 | 选型 | 关键属性 |
| --- | --- | --- |
| 轻量成功/失败提示，不打断用户 | Message | `Message.success()` `.error()` |
| 需要用户确认的警告/确认 | Modal 命令式 | `Modal.confirm()` |
| 右上角角标通知（可含操作按钮） | Notification | `Notification.open()` |
| 页面顶部常驻警告 | Alert | `type` `message` `closable` |
| 目标元素旁确认气泡 | Popconfirm | `content` `onClose` |
| 悬浮文字提示 | Tooltip | `overlay` `placement` |
| 内容加载中 | Spin | `spinning` `tip` |

## 决策 7: 选择人员/物料的参照方式

| 判断条件 | 选型 | 关键属性 |
| --- | --- | --- |
| 弹窗单选/多选 + 穿梭（待选区↔已选区） | RefTable (Pro) | `type="radio"/"checkbox"` `columns` `data` `fieldNames` |
| 左右双表格穿梭 | TableTransfer (Pro) | `leftColumns` `rightColumns` `data` |
| 简单列表穿梭 | Transfer | `dataSource` `targetKeys` `render` |
| 下拉+表格搜索选择 | InputSelect (Pro) | `columns` `dataSource` `multiple` |

## 决策 8: NextPro 支撑服务选择

| 业务场景 | 首选能力 | 推荐入口 |
| --- | --- | --- |
| 单据审批、审批按钮、字段权限、审批面板 | approval | `createApprovalRuntimeInstance` |
| 编码规则、自动生成单据编号、取号 | autoCode | `AutoCode` / `useAutoCode` |
| 暂存页面状态、保存草稿、恢复未提交数据 | draft | `openSaveDraftModal` / `openDraftManager` |
| MDF 模型参照选择、范围过滤 | mdfRefer | `MdfRefer` / `useRefer` |
| MDF 过滤查询、过滤面板、读取条件 | mdfFilter | `MdfFilterPanel` / `useFilter` |
| 单据打印、列表批量打印、打印预览 | print | `usePrint` |
| 文件上传、附件接入、临时附件绑定 | upload | `Upload` / `createUploadSession` |

## 决策 9: NextPro Layouts 选择

| 页面结构场景 | 首选组件 | 推荐入口 |
| --- | --- | --- |
| 列表页外壳，包含查询区、工具栏和表格 | ListLayout | `tne-tinpernextpro-fe/layouts` |
| 详情页外壳，包含头部、表单主体和底部操作 | DetailLayout | `tne-tinpernextpro-fe/layouts` |
| 子表、明细、分组内容页签 | LineTabs | `tne-tinpernextpro-fe/layouts` |
| 按钮工具栏、批量操作区、底部操作区对齐 | ToolbarLayout | `tne-tinpernextpro-fe/layouts` |
| 左侧树 + 右侧表格或卡片内容 | TreeTableLayout | `tne-tinpernextpro-fe/layouts` |
