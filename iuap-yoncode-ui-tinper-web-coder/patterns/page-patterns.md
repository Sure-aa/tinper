# 典型页面结构模式

> 以下模式均来自真实项目（安装器、云管理套件），仅供选型参考，不强制。

## 模式 1: 企业级列表页（最高频）

```
SearchForm（查询区）+ DataGrid（数据区）+ Modal（编辑/详情弹窗）
```

> 新建列表页数据区优先 **DataGrid**；改动已有列表页则保持其原组件（DataTable 等）不替换。下方 API 名以 DataTable 为例，DataGrid 对应能力见 `../references/DataGrid/readme.md`。

- SearchForm 根属性 `onSearch` 获取查询条件；根属性 `onReset` 处理重置，`submitter` 只定制按钮区
- 数据表格的 `request` 或 `params` 传入条件
- 数据表格 `operationItems`/`operations` 触发打开 Modal
- Modal 内 DataForm 渲染表单，`formMode` 控制编辑/浏览态

## 模式 2: 详情侧抽屉

```
DataGrid（新建）/ DataTable（已有）+ Drawer + DataForm formMode="browse"
```

## 模式 3: 工具栏

```
Space + Button(type="primary") + Button + Tooltip/Button + Popconfirm(危险操作)
```

真实项目中，工具栏几乎都用 Space 包裹 Button/ButtonGroup/Dropdown 组成。Dropdown.Button 用于带下拉菜单的操作按钮。

## 模式 4: 参照选择

```
Form.Item + RefTable（通过 value/onChange 与表单集成）
```

## 模式 5: Tab 页签 + 内容

```
Tabs → TabPane1: DataGrid / TabPane2: EditGrid / TabPane3: DataForm
```

> 新建表格优先 Grid 系列；改动已有 Tab 内表格则保持原组件（DataTable/EditTable）不替换。

## 模式 6: 折叠面板 + 表单组

```
Collapse → Panel: DataForm（基本信息）/ DataForm（扩展信息）
```

## 模式 7: HOC 链式组合（Base Table 旧模式）

```js
const ComposedTable = dragColumn(bigData(multiSelect(Table, Checkbox)))
```

外层包内层。仅在用户明确要求用 Base Table 灵活组合时使用；新建表格优先 DataGrid（内置拖拽/排序/大数据）。

## 模式 8: 主从联动（Master-Detail）

```
DataGrid（主表）+ DataGrid/EditGrid（从表）
```

> 新建主从表优先 Grid 系列；改动已有主从表则保持原组件（DataTable/EditTable）不替换。

- 主表 `operationTypeProps={{rowActiveKeysMode:'single'}}` + `rowActiveKeys` 控制行高亮
- 主表行点击 → 获取 `record.id` → 从表 `params` 或 `queryData()` 刷新

## 模式 9: 安装/配置向导页

```
Steps（步骤条）+ Collapse（折叠面板）+ Form（表单）+ Table（选择列表）
```

## 模式 10: 可拖拽侧边栏布局

```
Layout + Layout.Spliter + Sider + Content
```

Layout.Spliter 提供可拖拽调节宽度的侧边栏布局，真实项目中用于主面板+详情面板的左右分栏。
