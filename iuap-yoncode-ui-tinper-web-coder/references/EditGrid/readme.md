---
tags:
  - TinperNextPro
  - EditGrid组件
---

# EditGrid 编辑表格

<!--EditGrid-->
`EditGrid` 是 TinperNextPro 基于底层 `@tinper/grid` 封装的编辑表格组件。它不经过 `GridCompat`，不兼容旧 `EditTable` 属性名；展示、排序、过滤、列设置、行选择、行号、分页、合计、单元格选择、行拖拽等能力优先透传 TinperGrid 原生 API，行内编辑、展开表单、抽屉表单、校验、增删改、保存/取消、操作列、自动增行等编辑能力由 `EditGrid` 补齐。

## AI 使用原则

- 新建行内编辑、明细子表、增删行、批量填充、单元格校验、可编辑列表：优先用 `EditGrid`。
- 只读列表、请求分页、搜索工具栏、表格/卡片切换：用 `DataGrid`。
- 只需要底层 Grid 原生能力且不需要业务编辑状态管理：用 `TinperGrid` 的 `Grid`。
- 修改已有 `EditTable` 时不要主动迁移到 `EditGrid`，除非用户明确要求重构。
- 不要把旧 `EditTable` 的 `columns/editType/editOptions/editAbled/renderFormItem/addRow({ rowData })` 直接套给 `EditGrid`；`EditGrid` 使用 `columnDefs/editor/editorProps/editable/renderEditor/addRow(record, options)`。

## 快速使用

```tsx
import React, { useMemo, useRef, useState } from 'react';
import { Button, Space, Tag } from '@tinper/next-ui';
import { EditGrid } from 'tne-tinpernextpro-fe';

export default function MaterialEditGrid() {
  const gridRef = useRef<any>(null);
  const [data, setData] = useState([
    { id: '1', material: '显示器', category: 'device', qty: 2, enabled: true },
    { id: '2', material: '机械键盘', category: 'office', qty: 5, enabled: true },
  ]);

  const categoryOptions = [
    { label: '设备', value: 'device' },
    { label: '办公', value: 'office' },
  ];

  const columnDefs = useMemo(() => [
    {
      field: 'material',
      headerName: '物料名称',
      width: 180,
      editable: true,
      editor: 'input',
      editorProps: { placeholder: '请输入物料名称' },
      rules: [{ required: true, message: '物料名称不能为空' }],
    },
    {
      field: 'category',
      headerName: '分类',
      width: 140,
      editable: true,
      editor: 'select',
      editorProps: { options: categoryOptions },
      render: value => categoryOptions.find(item => item.value === value)?.label || '-',
    },
    {
      field: 'qty',
      headerName: '数量',
      width: 100,
      sortable: true,
      editable: true,
      editor: 'number',
      editorProps: { min: 1, precision: 0 },
      rules: [{ validator: value => value > 0 ? undefined : '数量必须大于 0' }],
    },
    {
      field: 'enabled',
      headerName: '启用',
      width: 100,
      editable: true,
      editor: 'switch',
      render: value => <Tag>{value ? '启用' : '停用'}</Tag>,
    },
  ], []);

  return (
    <>
      <Space style={{ marginBottom: 12 }}>
        <Button
          colors="primary"
          onClick={() => gridRef.current?.addRowLast({ material: '', category: 'office', qty: 1, enabled: true })}
        >
          新增行
        </Button>
        <Button onClick={() => gridRef.current?.validate()}>校验全部</Button>
        <Button onClick={() => console.log(gridRef.current?.getChangedRows())}>查看变更</Button>
      </Space>
      <EditGrid
        ref={gridRef}
        rowKey="id"
        data={data}
        columnDefs={columnDefs}
        editMode="inline"
        editTrigger="click"
        validateTrigger="onChange"
        autoAddRow={false}
        rowSelection={{ mode: 'multiRow', showSelectedFilter: true }}
        operationMode="hover"
        operationTypeProps={{ maxCount: 3, columnWidth: 100 }}
        operationColumn={{ width: 100, pinned: 'right' }}
        operations={[
          {
            key: 'copy',
            text: '复制',
            onClick: record => gridRef.current?.addRowAfter(record.id, {
              ...record,
              id: `copy-${Date.now()}`,
            }),
          },
        ]}
        onDataChange={(nextData) => setData(nextData)}
        height={380}
        width={980}
      />
    </>
  );
}
```

## 核心模型

| 旧 EditTable 概念 | EditGrid 写法 | 注意 |
|--|--|--|
| `columns` | `columnDefs` | 使用 TinperGrid 原生 `ColumnDef` 扩展编辑字段 |
| `title/dataIndex` | `headerName/field` | 支持 `field="a.b"` 读写嵌套值 |
| `type="inline"` | `editMode="inline"` | 单元格行内编辑 |
| `type="inlineForm"` | `editMode="expandForm"` | 展开行表单 |
| 抽屉编辑 | `editMode="drawerForm"` | 可自动按可编辑列生成表单 |
| `autoEditedByClickRows` | `editTrigger` | `'manual' \| 'click' \| 'hover'` |
| `editType` | `editor` | 内置编辑器名更丰富 |
| `editOptions` | `editorProps` | 可传对象或函数 |
| `editAbled` | `editable` | 拼写是 `editable` |
| `renderFormItem` | `renderEditor` | 接收 `{ value, record, rowIndex, column, setValue }` |
| `textToFormItemValue` | `valueParser` | 写入草稿前转换值 |
| `validator/patternMsg` | `rules` | `required/pattern/validator/message` |
| `operationItems` | `operations` | 每项自带 `onClick/render/hidden/disabled` |
| `addRow({ rowData })` | `addRow(record, options)` | 参数不再是对象包一层 |
| `getAllData` | `getData` | 返回已清理内部字段后的业务数据 |
| `getEditRows` | `getUpdatedRows` / `getChangedRows` | 新增、更新、删除分开追踪 |

## 默认行为

`EditGrid` 为编辑表格默认开启一组常用能力，业务可继续传 `false` 或自定义配置覆盖：

| 能力 | 默认值 |
|--|--|
| `rowSelection` | `{ mode: 'multiRow', showSelectedFilter: false }` |
| `showRowNum` | `{ width: 58, pinned: 'left' }` |
| `pagination` | **`false`（关闭）**；传 `true` 时为 `{ current: 1, pageSize: 10 }` |
| `enableSorting` / `enableFilter` / `enableFind` / `enableColumnSet` | `true` |
| `columnSetOptions` | 底部按钮全开（footer/全选/已选/列宽/列顺序/重置/置顶/锁定）|
| `suppressResizeColumns` | `true` |
| `cellSelection` / `popMenu` | 默认开启（多区域选择、拖拽扩展、拖拽柄、右键菜单）|
| `summary` | **`false`（关闭）**；传 `true` 时为小计+合计、合计固定底部、千分位 |
| `autoMerge` / `openMergeCell` | **`false`** |
| `operationMode` | `'column'` |
| `operationType` | 未传时由 `operationMode` 推导（`fixed`→`fixed`，否则 `button`）|
| `autoAddRow` | `true` |
| `singleEditRow` | `true`（同一时刻只允许一行编辑）|

如果不想出现空白自动行，明确传 `autoAddRow={false}`。需要分页 / 合计 / 合并时分别传 `pagination` / `summary` / `autoMerge`；不需要选择、单元格选择时传 `rowSelection={false}`、`cellSelection={false}`。

> ⚠️ **升级注意（breaking）**：`enableFilter` 默认 `true`，且会对未显式声明 `filter` 的列**自动推断筛选器**（number→numberFilter、date 类→dateFilter、其余→textFilter）。从旧版升级若不希望列上自动冒出筛选入口，传 `enableFilter={false}`。

## 模块加载

`EditGrid` 不注册 `AllModules`。组件会把默认能力和用户配置合并后，自动推导 TinperGrid 模块并动态加载，再和 `modules` 按 `moduleName` 去重合并。

常见自动模块：

| 配置/默认能力 | 自动模块 |
|--|--|
| 默认分页 | `PaginationModule` |
| 默认行选择 | `RowSelectionModule` |
| 默认行号 | `RowNumbersModule` |
| 默认合计 | `SummaryModule` |
| 默认列设置/排序/筛选/查找 | `ColumnSetModule`、`ColumnSortModule`、`FilterModule`、`ColumnFindModule` |
| 默认列宽拖拽 | `ColumnAutoSizeModule` |
| 默认单元格选择、右键菜单 | `CellSelectionModule` |
| 默认合并单元格 | `MergeCellsModule` |
| `operationMode="hover"` | `RowHoverModule` |
| `editMode="expandForm"` | `TreeModule` |
| `rowDrag` | `RowDragModule` |
| 列 `pinned` 或操作列固定 | `ColumnPinnedModule` |

只有自动推导覆盖不到的底层能力才手动追加 `modules`。

## 编辑模式

| `editMode` | 行为 | 推荐场景 |
|--|--|--|
| `inline` | 单元格内直接渲染编辑器 | 最常用，明细子表、数量金额录入 |
| `expandForm` | 行展开后渲染 `renderEditForm` | 字段较多但仍希望留在表格上下文 |
| `drawerForm` | 右侧抽屉编辑；未传 `renderEditForm` 时按可编辑列生成表单 | 字段多、需要独立编辑空间 |

`editTrigger`：

- `manual`：只通过默认操作列的“编辑”或 `ref.editRow(key)` 进入编辑。
- `click`：点击行进入编辑。
- `hover`：鼠标移入行进入编辑；配 `autoSaveOnRowHoverOut` 可移出自动保存。

`expandForm/drawerForm` 自定义表单示例：

```tsx
<EditGrid
  editMode="drawerForm"
  renderEditForm={({ record, setRecord }) => (
    <Input
      type="textarea"
      value={record.memo}
      onChange={value => setRecord({ memo: value })}
    />
  )}
/>
```

## 编辑器

内置 `editor`（`BuiltInEditorType`）：

`input`、`textarea`、`select`、`number`、`inputNumberGroup`、`switch`、`date`、`dateTime`/`datetime`、`time`、`rangePicker`/`rangepicker`、`cascader`、`radio`/`radiogroup`、`checkbox`/`checkboxgroup`、`treeSelect`/`treeselect`、`custom`。

> `refTable`/`refTree`/`refTableTree` **已不是内置 editor**（已从 `BuiltInEditorType` 移除）。它们现在作为**任意字符串 editor**，通过下方「自定义 / 参照编辑器」注入。所有内置 editor 写入前都会过列级 `valueParser`。

### 自定义 / 参照编辑器

去掉强绑定后，接入任意受控组件（参照、多语输入、业务控件）有三条等价通道，优先级：**列级 `editorProps.component` > 列级 `editorProps.referComponent` > 全局 `editorComponents[editor]` > 内置回退 `Input`**。

列级注入：

```tsx
{
  field: 'supplier',
  headerName: '供应商',
  editable: true,
  editor: 'refTable',            // 任意字符串，触发组件注入
  editorProps: {
    referComponent: RefTable,    // 或 component: RefTable
    valuePropName: 'value',      // 受控值字段名，默认 'value'（Switch 用 'checked'）
    changePropName: 'onChange',  // 变化回调字段名，默认 'onChange'
    getValueFromChange: (value, selected) => selected?.code,  // 从回调参数抽取写入值
    // 其余 props 透传给组件
  },
}
```

全局注册（多列复用同一组件时更省）：

```tsx
<EditGrid
  editorComponents={{
    refTable: RefTableEditor,
    bizProduct: ProductSelector,
  }}
  columnDefs={[
    { field: 'supplier', editor: 'refTable', editable: true },
    { field: 'product', editor: 'bizProduct', editable: true },
  ]}
/>
```

需要完全自定义渲染时仍可用 `renderEditor`（优先级最高）：

```tsx
{
  field: 'supplier', headerName: '供应商', editable: true,
  renderEditor: ({ value, setValue }) => <RefTable value={value} onChange={next => setValue(next)} />,
}
```

## 浏览态与单行编辑

- **`browseMode`（默认 `false`）**：纯浏览态，强制把 `editTrigger` 降为 `'manual'`、关闭自动增行/操作列/行拖拽/外部点击保存，`editRow` 直接返回 `false`。保留排序、过滤、选择等纯浏览能力。与 `editMode` 正交（抽屉/展开表单在 browseMode 下不渲染）。
- **`singleEditRow`（默认 `true`）**：同一时刻只允许一行处于编辑态；进入新行编辑前会先尝试保存当前编辑行（校验失败则不切换）。设为 `false` 可同时编辑多行。
- **`fillSpace`**：已支持，与 `DataGrid` 一致地解析 `width/height/fillSpace`（未传且无尺寸时默认填满，传尺寸则尺寸优先）。

> ⚠️ **外部点击自动保存校验**与 `singleEditRow` **耦合**：当 `singleEditRow=true`（默认）且非 `drawerForm`、非 `browseMode` 时，点击表格外部会触发当前编辑行的保存校验。**没有独立开关**只关外部保存而保留单行编辑；要关掉只能设 `singleEditRow={false}`、改用 `editMode="drawerForm"` 或 `browseMode`。

## 自动增行

`autoAddRow` 默认 `true`：

- 空数据初始化时显示一条空白行。
- 编辑最后一行时自动追加下一条空白行。
- 未修改的自动空白行不会出现在 `getData()`、`onDataChange`、`getAddedRows()`、`validate()` 的业务数据中。
- 自动行被修改保存后转为真实新增行。
- `newRowFactory` 可提供默认值；组件会记录默认值快照，只有用户改动后才算新增。

```tsx
<EditGrid
  autoAddRow
  newRowFactory={() => ({ qty: 1, enabled: true })}
/>
```

如果页面有独立“新增行”按钮，通常传 `autoAddRow={false}`，避免用户看到额外空白行。

## 操作区

| 配置 | 说明 |
|--|--|
| `defaultOperationVisible` | 是否显示默认“编辑/删除/保存/取消” |
| `operations` | 自定义操作项，会追加到默认操作后 |
| `operationMode="column"` | 始终显示右侧操作列 |
| `operationMode="hover"` | 行 hover 显示操作；收起后转为右侧固定列 |
| `operationMode="fixed"` | 始终使用右侧固定操作列/更多菜单 |
| `operationType` | `'button' \| 'link' \| 'fixed' \| Function` |
| `operationTypeProps.maxCount` | 外露操作数，超过进入更多 |
| `operationTypeProps.folded` | hover 模式初始是否收起 |
| `operationTypeProps.columnWidth` | 收起/固定列宽 |
| `operationColumn={false}` | 隐藏操作列；若 `operationMode="hover"` 未收起时也不会渲染列 |

默认操作在编辑态为“保存/取消”，非编辑态为“编辑/删除”。`editMode="drawerForm"` 下默认操作保持“编辑/删除”，保存/取消在抽屉 footer 中（footer 固定，不可自定义）。

`operationColumn` 还可传 `filter`/`sortable`/`columnSetAble`（均默认 `false`），让操作列参与筛选 / 排序 / 列设置；默认不参与，避免被全局筛选误处理。

## API

`EditGridProps` 继承 `@tinper/grid` 的 `GridProps`，但重定义 `data`、`columnDefs`。未列出的属性继续透传底层 Grid。

| 参数 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `data` | `T[]` | `[]` | 表格数据 |
| `columnDefs` | `EditGridColumnDef[]` | - | 编辑列定义 |
| `rowKey` | `string \| (record) => string` | `'id'` | 业务行唯一标识 |
| `editMode` | `'inline' \| 'expandForm' \| 'drawerForm'` | `'inline'` | 编辑模式 |
| `editTrigger` | `'manual' \| 'click' \| 'hover'` | `'manual'` | 进入编辑态方式 |
| `browseMode` | `boolean` | `false` | 浏览态，关闭一切编辑入口（详见「浏览态与单行编辑」）|
| `singleEditRow` | `boolean` | `true` | 同一时刻只允许一行编辑（与外部点击保存耦合）|
| `editorComponents` | `Record<string, ComponentType>` | - | 按 `editor` 类型全局注册自定义编辑组件 |
| `validateTrigger` | `'onChange' \| false` | `false` | 值变化时是否校验 |
| `autoSaveOnRowHoverOut` | `boolean` | `false` | hover 编辑移出自动保存 |
| `autoAddRow` | `boolean` | `true` | 自动空白增行 |
| `resetStateOnDataChange` | `boolean` | `false` | 外部数据变化时是否清空编辑/变更/错误状态 |
| `newRowFactory` | `() => Partial<T>` | - | 新增行默认值 |
| `renderEditForm` | `(context) => ReactNode` | - | 展开/抽屉表单自定义内容 |
| `drawerProps` | `Partial<DrawerProps>` | - | 抽屉表单属性，不含 `show/visible/onClose/children/footer/title`；footer 固定为保存/取消，不可自定义 |
| `drawerTitle` | `ReactNode \| (record, rowIndex) => ReactNode` | `'编辑'` | 抽屉标题 |
| `operations` | `EditGridOperation[]` | - | 自定义操作项 |
| `operationMode` | `'column' \| 'hover' \| 'fixed'` | `'column'` | 操作展示模式 |
| `operationType` | `'button' \| 'link' \| 'fixed' \| Function` | 由 `operationMode` 决定 | 操作渲染类型 |
| `operationTypeProps` | `{ maxCount?; folded?; columnWidth? }` | - | 操作区扩展配置 |
| `operationColumn` | `false \| { field?; headerName?; width?; pinned? }` | `{ width: 180, pinned: 'right' }` | 操作列配置 |
| `defaultOperationVisible` | `boolean` | `true` | 默认操作是否显示 |
| `onDataChange` | `(data, context) => void` | - | 数据变化回调，context.type 为 `add/update/delete/save/cancel/reorder/clear` |
| `onRowSave` | `(record, data) => void` | - | 行保存 |
| `onRowDelete` | `(records, data) => void` | - | 行删除 |
| `onValidate` | `(valid, errors) => void` | - | 校验回调 |

### Column

`EditGridColumnDef` 继承 TinperGrid `ColumnDef`。

| 参数 | 类型 | 说明 |
|--|--|--|
| `editable` | `boolean \| (record, rowIndex) => boolean` | 单元格是否可编辑 |
| `editor` | `EditorType` | 内置编辑器类型 |
| `editorProps` | `Record<string, any> \| (record, rowIndex, column) => Record<string, any>` | 编辑器属性 |
| `renderEditor` | `(context) => ReactNode` | 自定义编辑器 |
| `valueParser` | `(value, record, rowIndex, column) => any` | 写入草稿前转换 |
| `rules` | `EditGridRule[]` | 校验规则 |

### Rule

| 参数 | 类型 | 说明 |
|--|--|--|
| `required` | `boolean` | 是否必填 |
| `message` | `string` | 错误文案 |
| `pattern` | `RegExp` | 正则校验 |
| `validator` | `(value, record, data) => string \| void \| Promise<string \| void>` | 返回字符串表示失败 |

### Operation

| 参数 | 类型 | 说明 |
|--|--|--|
| `key` | `string` | 唯一标识 |
| `text` | `ReactNode` | 文案 |
| `hidden` | `boolean \| (record, rowIndex, editing) => boolean` | 是否隐藏 |
| `disabled` | `boolean \| (record, rowIndex, editing) => boolean` | 是否禁用 |
| `onClick` | `(record, rowIndex, editing) => void` | 点击回调 |
| `render` | `(record, rowIndex, editing, operation) => ReactNode` | 自定义渲染 |

## Ref

| 方法 | 说明 |
|--|--|
| `api` | 底层 TinperGrid `GridApi` |
| `addRow(record?, options?)` | 新增行，`options.index` 指定插入位置，`options.edit` 控制是否立即编辑 |
| `addRowFirst(record?, options?)` / `addRowLast(record?, options?)` | 首行/末行新增 |
| `addRowBefore(rowKey, record?, options?)` / `addRowAfter(rowKey, record?, options?)` | 指定行前/后新增 |
| `addRowChild(rowKey, record?, options?)` | 作为子行新增 |
| `updateRow(rowKey, patch)` | 更新行 |
| `updateCellValue(rowKey, field, value)` | 更新单元格 |
| `updateColumn(field, value)` | 更新整列 |
| `updateColumnUp(rowKey, field, value, count?)` / `updateColumnDown(...)` | 从指定行向上/向下填充 |
| `updateCells(updates)` | 批量更新单元格 |
| `deleteRows(rowKeys)` | 删除一行或多行 |
| `editRow(rowKey)` / `saveRow(rowKey)` / `cancelRow(rowKey)` | 编辑、保存、取消；`saveRow` 返回校验结果 |
| `clearEditRows()` / `clearData()` | 清空编辑态/清空数据 |
| `moveRows(rowKeys, targetRowKey, position?)` | 移动行 |
| `validate(rowKey?)` | 校验指定行或全部行 |
| `getData()` | 当前业务数据，不含内部字段和未改动自动空白行 |
| `getRowData(rowKey)` / `getCellValue(rowKey, field)` | 获取行/单元格 |
| `getEditingRowKeys()` | 编辑中的行 key |
| `getAddedRowKeys()` / `getAddedRows()` | 新增 |
| `getUpdatedRowKeys()` / `getUpdatedRows()` | 更新 |
| `getDeletedRowKeys()` / `getDeletedRows()` | 删除 |
| `getChangedRows()` | 新增和更新后的变更行，不含删除行 |
| `getSelectedRowKeys()` / `getSelectedRows()` / `setSelectedRowKeys(keys)` / `clearSelection()` | 选择 |
| `getErrors()` / `setErrors(errors)` | 错误读写 |
| `setCellError(rowKey, field, message?)` / `getCellError(rowKey, field)` / `clearCellError(rowKey?, field?)` | 单元格错误 |

## 易踩坑

- `EditGrid` 传给底层 Grid 的 `rowKey` 固定为内部 `__edit_grid_key__`。业务代码和 ref 方法仍使用你传入的业务 `rowKey` 值；直接调用 `api` 时注意底层 key 可能不是原始字段名。
- `rowKey` 默认 `'id'`，新增、编辑、删除、选择、变更追踪都依赖它；数据没有 `id` 必须显式传。
- `autoAddRow` 默认 `true`，空表会出现一条空白行；不想要时必须传 `autoAddRow={false}`。
- `addRow(record, options)` 默认在 `autoAddRow=true` 时不会立即进入编辑态；需要立即编辑时传 `{ edit: true }`，或关闭自动增行。
- `getChangedRows()` 不包含删除行；提交保存时通常同时读取 `getAddedRows()`、`getUpdatedRows()`、`getDeletedRows()`。
- `validate()` 会跳过未改动的自动空白行，这是预期行为。
- `renderEditor` 的自定义组件必须按受控组件实现 `value/onChange`，并调用 `setValue`，否则草稿和校验不会更新。
- `editorProps.onChange` 会在内部 `setValue` 后继续执行；不要在其中再次直接改表格 data 导致重复状态。
- `resetStateOnDataChange=false` 时，外部 `data` 刷新不会清空编辑态、变更状态、错误；重新加载远端数据通常应设为 `true`。
- 列宽拖拽使用 TinperGrid 原生 `suppressResizeColumns/keepWidthBalance/onColumnResizeEndCallback`；旧 `dragborder/onDropBorder` 是兼容层习惯，不要优先用于 `EditGrid`。
- `operationMode="hover"` 会合并 `rowHover`；如果用户自定义了 `rowHover.rowHoverContent`，默认 hover 操作可能不显示。
- 参照编辑器类型不会自动生成完整参照组件，必须使用 `renderEditor` 接入 `RefTable`、`RefTree` 等。
