---
tags:
  - TinperNextPro
  - DataGrid组件
---

# DataGrid 数据表格

<!--DataGrid-->
`DataGrid` 是 TinperNextPro 基于底层 `@tinper/grid` 封装的数据表格组件。它不经过 `GridCompat`，不兼容旧 `DataTable` 属性名；列、排序、过滤、列设置、行选择、行号、合计、行 hover、滚动等能力优先透传 TinperGrid 原生 API，搜索区、操作列、查看已选、卡片/看板视图、表头明细切换、二维表、行号列、链接穿透等业务能力由 `DataGrid` 补齐。

> **数据是外部驱动的**：`DataGrid` 自身**不做异步请求**，数据通过 `data` prop 传入。需要服务端分页/排序时，由调用方监听分页等回调、自行请求后回填 `data`（见「数据与分页」）。

## AI 使用原则

- 新建普通业务列表页、分页列表、带搜索工具栏的表格、表格/卡片/看板视图、跨页勾选、操作列：优先用 `DataGrid`。
- 用户明确要行内编辑、增删行、子表明细编辑：改用 `EditGrid`。
- 用户明确要底层 `@tinper/grid`、手动注册模块、最轻量普通表格：用 `TinperGrid`。
- 修改已有 `DataTable` 时不要主动迁移到 `DataGrid`，除非用户明确要求重构。
- 不要把 `DataTable` 的 `columns/dataIndex/operationItems/queryData` 直接套给 `DataGrid`；`DataGrid` 使用 `columnDefs/field/operations`。
- 不要给 `DataGrid` 传 `request/autoLoad`，也不要调用 `ref.query()`/`ref.reset()`——这些方法不存在。数据只认 `data` prop。

## 快速使用

```tsx
import React, { useMemo, useRef, useState } from 'react';
import { Button, Input, Space, Tag } from '@tinper/next-ui';
import { DataGrid } from 'tne-tinpernextpro-fe';

const allOrders = Array.from({ length: 57 }, (_, index) => ({
  id: String(index + 1),
  code: `SO-${String(index + 1).padStart(4, '0')}`,
  customer: ['华北客户', '华东客户', '华南客户'][index % 3],
  amount: 1000 + index * 37,
  status: index % 4 === 0 ? '已关闭' : '进行中',
}));

export default function OrderList() {
  const gridRef = useRef<any>(null);
  const [keyword, setKeyword] = useState('');
  const [data, setData] = useState(allOrders);
  const [selectedRowKeys, setSelectedRowKeys] = useState<string[]>([]);

  const columnDefs = useMemo(() => [
    { field: 'code', headerName: '单据编号', width: 160, pinned: 'left', sortable: true },
    { field: 'customer', headerName: '客户', width: 180, filter: true },
    { field: 'amount', headerName: '金额', width: 120, align: 'right', sortable: true },
    { field: 'status', headerName: '状态', width: 120, render: value => <Tag>{value}</Tag> },
  ], []);

  // 前端过滤示例；服务端场景请在 pagination.onChange 里请求后 setData
  const filtered = useMemo(
    () => allOrders.filter(item => !keyword || item.code.includes(keyword)),
    [keyword],
  );

  return (
    <DataGrid
      ref={gridRef}
      rowKey="id"
      columnDefs={columnDefs}
      data={filtered}
      pagination={{ current: 1, pageSize: 20, showTotal: total => `共 ${total} 条` }}
      rowSelection={{
        mode: 'multiRow',
        selectedRowKeys,
        showSelectedFilter: true,
        onChange: event => setSelectedRowKeys(event.selectedKeys || []),
      }}
      searchPanel={(
        <Space>
          <Input value={keyword} onChange={setKeyword} placeholder="搜索单号" />
          <Button colors="primary" onClick={() => setData(filtered)}>查询</Button>
          <Button onClick={() => { setKeyword(''); setData(allOrders); }}>重置</Button>
        </Space>
      )}
      operations={[
        { key: 'view', text: '查看', onClick: record => console.log(record) },
        { key: 'edit', text: '编辑', disabled: record => record.status === '已关闭' },
      ]}
      operationColumn={{ width: 160, pinned: 'right' }}
      height={420}
    />
  );
}
```

## 数据与分页

`DataGrid` 是 `data` 驱动，不内置异步请求：

- **静态/前端数据**：直接传 `data`；排序、过滤、分页默认在底层 Grid 内本地完成。
- **服务端分页/排序**：监听 `pagination.onChange`（以及排序/过滤变化回调），由调用方请求对应页数据，再回填 `data`。

```tsx
const [data, setData] = useState([]);
const [pagination, setPagination] = useState({ current: 1, pageSize: 20 });

const loadPage = async (current, pageSize) => {
  const res = await fetchOrders({ page: current, pageSize });
  setData(res.list);
  setPagination(p => ({ ...p, current, pageSize }));
};

<DataGrid
  data={data}
  pagination={{
    ...pagination,
    total: totalCount,
    onChange: (current, pageSize) => loadPage(current, pageSize),
  }}
/>
```

- `ref.reload()` 只是用当前 `data` 重新刷进内部 state（含行号重算），**不发请求**。
- 需要重新拉数据时，调用方自己请求后再 `setData`。

## 默认行为

`DataGrid` 默认开启一组常用能力，业务可传 `false` 或自定义配置覆盖：

| 能力 | 默认值 |
|--|--|
| `pagination` | `{ current: 1, pageSize: 20 }` |
| `rowSelection` | `{ mode: 'multiRow' }` |
| `showSelectedFilter` | `true` |
| `enableSorting` / `enableFilter` / `enableFind` / `enableColumnSet` / `enablePinned` | `true` |
| `columnSetOptions` | 底部按钮全开（footer/全选/已选/列宽/列顺序/重置/置顶/锁定）|
| `cellSelection` | 多区域选择 + 拖拽扩展 + 拖拽柄 |
| `showRowNum` | `true`（行序号；与业务「行号列」`lineNo` 不同）|
| `operationMode` | `'hover'`（鼠标移入行显示操作）|
| `suppressMovableColumns` / `suppressResizeColumns` | `true`（默认**禁用**拖拽列顺序 / 拖拽改列宽）|
| `enableFillRemainingWidth` | `true` |
| `activeRowMode` | `'single'`，`activeOnRowClick` 默认 `true` |

> 注意：列顺序拖拽、列宽拖拽**默认是关闭的**（`suppressMovableColumns`/`suppressResizeColumns` 默认 `true`）。需要时显式传 `false`，或用 `dragborder`/`draggable` 等列宽能力。

## 视图模式：表格 / 卡片 / 看板

通过 `displayMode` 在三种视图间切换（替代旧版 `viewMode/renderCard/cardLayout`，旧属性已废弃）：

```tsx
<DataGrid
  data={data}
  defaultDisplayMode="table"
  displayModeSwitchVisible          // 显示 表格/卡片/看板 切换 Radio
  cardConfig={{
    titleField: 'code',
    statusField: 'status',
    imageField: 'avatar',
    showSelectAll: true,
    pageSize: 12,
  }}
  kanbanConfig={{
    groupField: 'status',           // 按状态分列
    groupList: [                    // 预定义分组顺序与空组
      { value: '进行中', text: '进行中' },
      { value: '已关闭', text: '已关闭' },
    ],
    defaultPageSize: 10,
  }}
/>
```

| 配置 | 受控 | 说明 |
|--|--|--|
| `displayMode` | 是 | `'table' \| 'card' \| 'kanban'`，非法值归一为 `table` |
| `defaultDisplayMode` | 否 | 默认 `'table'`；也可在 `cardConfig.defaultMode` / `kanbanConfig.defaultMode` 配置 |
| `displayModeSwitchVisible` | — | 是否显示切换 Radio，默认 `false`（仅当 cardConfig/kanbanConfig 任一 `switchVisible:true` 时才显示）|

**卡片视图 `cardConfig`**：`titleField`（标题列，未传取首列）、`statusField`+`showStatus`（状态徽标，可用 `statusStyle`）、`imageField`（左侧图）、`showSelectAll`（本页全选）、`pageSize`、`mode`/`defaultMode`/`switchVisible`/`onModeChange`/`onCardJointCellQuery`。字段渲染：剔除标题/状态/图片/操作列后，其余列以 `label: value` 铺开；列上 `cardLabelVisible:false` 可隐藏 label。

**看板视图 `kanbanConfig`**：`groupField`（必填，分组依据）、`groupList`（`{value,text}[]` 预定义分组顺序+占位空组）、`groupValueField`/`groupTextField`（自定义 groupList 取值键）、`defaultPageSize`、`mode`/`defaultMode`/`switchVisible`/`onModeChange`/`onGroupPageInfoChange`。每个分组一列，列头显示分组名+计数，列内逐行渲染卡片。

> 卡片/看板视图里操作按钮 `maxCount` 默认 `3`（表格操作列默认 `5`）。

## 表头 / 表头+明细切换（sumSwitch）

同一份 `columnDefs` 在「只看表头列」与「表头+明细列」之间切换，适合主子表场景：

```tsx
<DataGrid
  sumSwitch={{
    defaultValue: true,              // true=只看表头（默认），false=表头+明细
    detailColumnFields: ['qty', 'price', 'memo'],  // 指定明细列
    // 或用 isDetailColumn: col => ... 自定义判定
    onChange: (value, ctx) => console.log(value, ctx.selectedRowKeys),
  }}
/>
```

`DataGridSumSwitchConfig` 关键字段：`value`/`defaultValue`（默认 `true`）、`keys`（不同模式用不同 `rowKey`：`{true,false,header,detail}`）、`options`（自定义 Radio 文案）、`visible`、`hideDetailColumns`（默认 `true`）、`detailColumnFields`/`isDetailColumn`（判定明细列）、`clearSelectionOnChange`（默认 `true`）、`onBeforeChange`/`onChange`。

## 二维表（table2D）

把长表透视成宽表（行=行维度，列=列维度×指标），如销售数据按 [地区]×[产品] 透视：

```tsx
<DataGrid
  table2D={{
    rowFields: ['region'],           // 行维度
    columnFields: ['product'],       // 列维度
    crossFields: ['amount'],         // 展开到交叉单元格的指标
    defaultShow2D: false,            // 默认 1D，可切 2D
    editable: true,                  // 二维单元格可编辑，回写到源数据
    onCellChange: ctx => console.log(ctx),
  }}
/>
```

`DataGridTable2DConfig` 关键字段：`rowFields`/`columnFields`/`crossFields`/`measureFields`（附加度量列）、`show2D`/`defaultShow2D`（默认 `false`）、`switchVisible`（默认 `true`）、`switchOptions`（默认 1D/2D）、`editable`（默认 `true`）/`crossFieldEditable`、`onBeforeCellChange`/`onCellChange`/`onShow2DChange`、`valueGetter`/`valueSetter`、`hideSum`/`subtotalText`/`totalText` 等。开启 2D 后组件用透视后的 data/columnDefs/summary 替代原始。

## 行号列（lineNo）

为带行号语义的列（如 `cControlType:'lineno'`）自动生成业务行号，常用于可增删行的单据：

```tsx
<DataGrid
  lineNo={{
    field: 'lineNo',                 // 行号字段；未传则自动找 cControlType==='lineno' 的列
    step: 10,                        // 步长，默认 10
    generateType: 'auto',            // 'auto'(连续编号) | 'binary'(折半插入，便于中间插行)
    onDataChange: (nextData, ctx) => console.log(ctx.type),
  }}
/>
```

- `generateType`：`1`/`'auto'` → 连续编号 `(index+1)*step`；`2`/`'binary'` → 折半插入编号（前后行号取中值，便于后续在中间插行）。
- 通过 ref 增删行时可带 `options.generateLineNo`（默认 `true`）：`setDataSource(rows, { generateLineNo: true })`、`appendRow(row, options)`、`insertRow(index, row, options)`。
- `ref.regenerateLineNo()` 按当前 generateType 全量重生成。

## 空状态（emptyConfig）

区分两种空：**数据源本身为空**（`empty`）与**有数据但筛选/搜索无结果**（`searchEmpty`）：

```tsx
<DataGrid
  emptyConfig={{
    emptyText: '暂无订单',
    searchEmptyText: '没有符合条件的订单',
    extra: <Button>新建订单</Button>,                 // 数据源为空时下方内容
    searchExtra: <Button onClick={clearFilter}>清空筛选</Button>,
  }}
/>
```

`DataGridEmptyConfig`：`emptyText`/`searchEmptyText`（未传回退 `emptyText`）、`extra`/`searchExtra`（`ReactNode` 或 `(type)=>ReactNode`，分别对应两种场景）。其余属性透传给底层 `<Empty>`（如 `description`/`image`）。仅表格模式生效，卡片/看板各自渲染空态。

## 链接穿透（jointQuery）

把单元格值渲染成可点击链接，点击穿透打开对应单据详情（如订单列表点单号开订单详情）。支持**组件级**和**列级**双重配置：

```tsx
<DataGrid
  jointQuery={{
    enabled: true,
    billtype: 'saleOrder',           // 单据类型（字段名或字面量）
    keyField: 'id',                  // 主键字段
    openType: 'new',                 // 'current' | 'new' | 'service'
    hasPermission: ctx => true,      // 权限校验
    beforeJointQuery: ctx => true,   // 返回 false 阻断
  }}
/>
```

列级：在 `columnDefs` 上设 `column.bJointQuery = true` 或 `column.jointQueryOpt = {...}`。`DataGridJointQueryConfig` 关键字段：`enabled`、`billtype`/`billno`、`keyField`/`rowId`、`openType`、`hasPermission`/`onNoPermission`、`beforeJointQuery`/`onJointQuery`/`open`（返回 false 阻断/自定义）、`asyncField`/`resolveAsyncBillInfo`（异步解析单据）、`serviceCode`/`domainKey`/`newOpen`。

## fillSpace

控制表格是否填满父容器（不是简单透传，DataGrid 自行解析 `width/height/fillSpace`）：

| 传入 | 结果 |
|--|--|
| `fillSpace={true}` | 填满父容器，忽略 width/height |
| `fillSpace` 未传 且 width/height 都未传 | 默认 `{ fillSpace: true }`（兼容旧 DataTable）|
| `fillSpace={false}`，或未传但传了任一尺寸 | `{ fillSpace: false }` + 透传显式尺寸 |

> 即「显式尺寸优先」：传了 `width` 就不会被默认 fillSpace 覆盖。

## 操作列

| `operationMode` | 表现 | 适用 |
|--|--|--|
| `hover`（默认） | 操作列隐藏，按钮浮在 hover 行右侧；可手动「显示固定操作列」| 默认列表 |
| `column` | 始终渲染右侧操作列 | 操作少、希望常驻 |
| `fixed` | 初始即为折叠的固定操作列/更多菜单 | 操作多 |

`operationColumn` 实际生效字段：`field`/`headerName`/`width`（默认 `160`）/`pinned`（默认 `'right'`）/`maxCount`（表格默认 `5`，超出折进「更多」）。`operationColumn={false}` 隐藏操作列；未传 `operations` 时不生成操作列。

## 模块加载

`DataGrid` 不注册 `AllModules`。组件会根据配置自动推导并动态加载必要模块，再和用户传入的 `modules` 按 `moduleName` 去重合并。

自动推导规则：

| 配置 | 自动模块 |
|--|--|
| `pagination` | `PaginationModule` |
| `rowSelection` | `RowSelectionModule` |
| `showRowNum` | `RowNumbersModule` |
| `summary` | `SummaryModule` |
| `rowDrag` | `RowDragModule` |
| `rowHover`、`operationMode='hover'` | `RowHoverModule` |
| `rowPinned` | `RowPinnedModule` |
| `rowStyle`、`getCellClassName`、激活行 | `RowStyleModule` |
| `cellSelection`、`popMenu`、`onPopMenuClick` | `CellSelectionModule` |
| `treeData`、展开行相关属性 | `TreeModule` |
| `enableColumnSet`、`columnSetOptions` | `ColumnSetModule` |
| `enableSorting`、列 `sortable/sort/sortIndex/sortBackend` | `ColumnSortModule` |
| `enableFilter`、列 `filter` | `FilterModule` 及对应 Text/Number/Date/Set/Custom/Multi Filter |
| `enablePinned`、列 `pinned`、右侧操作列 | `ColumnPinnedModule` |
| `enableFind`、列 `find/findable` | `ColumnFindModule` |
| `suppressResizeColumns=false` / `dragborder` | `ColumnAutoSizeModule` |
| `autoMerge`、列 `autoMergeColumn/rowSpan/colSpan` | `MergeCellsModule` |

只有在自动推导覆盖不到的底层能力才手动追加模块：

```tsx
import { RowPinnedModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowpinned';

<DataGrid rowPinned={{ topData }} modules={[RowPinnedModule]} />
```

## API

`DataGridProps` 继承 `@tinper/grid` 的 `GridProps`，但重定义了 `data`、`columnDefs`、`pagination`、`rowSelection`、`emptyConfig`。未列出的属性继续透传底层 Grid。

| 参数 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `data` | `T[]` | `[]` | 数据源（**唯一数据入口**，组件不做异步请求）|
| `columnDefs` | `ColumnDef[]` | `[]` | TinperGrid 原生列定义 |
| `pagination` | `false \| DataGridPaginationConfig` | `{ current:1, pageSize:20 }` | 分页配置；`onChange` 由调用方处理服务端分页 |
| `rowSelection` | `GridProps['rowSelection']` | `{ mode:'multiRow' }` | 行选择配置 |
| `emptyConfig` | `DataGridEmptyConfig` | - | 空状态（数据空/搜索无结果区分）|
| `selectedData` | `T[]` | - | 预置跨页已选数据 |
| `searchPanel` | `ReactNode` | - | 表格上方搜索区 |
| `operations` | `DataGridOperation[] \| (record, index) => DataGridOperation[]` | - | 操作项 |
| `operationMode` | `'column' \| 'hover' \| 'fixed'` | `'hover'` | 操作展示模式 |
| `operationColumn` | `false \| { field?; headerName?; width?; pinned?; maxCount? }` | `{ width:160, pinned:'right' }` | 操作列配置 |
| `showSelectedFilter` | `boolean` | `true` | 上方工具栏查看已选按钮 |
| `showSelectedOnly` | `boolean` | - | 受控查看已选 |
| `defaultShowSelectedOnly` | `boolean` | `false` | 非受控默认查看已选 |
| `activeRowKeys` | `Key[]` | - | 受控激活行 |
| `defaultActiveRowKeys` | `Key[]` | `[]` | 默认激活行 |
| `activeRowMode` | `'single' \| 'multiple'` | `'single'` | 激活行模式 |
| `activeOnRowClick` | `boolean` | `true` | 点击行是否更新激活行 |
| `displayMode` | `'table' \| 'card' \| 'kanban'` | - | 受控视图模式 |
| `defaultDisplayMode` | `'table' \| 'card' \| 'kanban'` | `'table'` | 默认视图模式 |
| `displayModeSwitchVisible` | `boolean` | `false` | 显示视图切换 Radio |
| `cardConfig` | `DataGridCardConfig` | - | 卡片视图配置 |
| `kanbanConfig` | `DataGridKanbanConfig` | - | 看板视图配置 |
| `sumSwitch` | `boolean \| DataGridSumSwitchConfig` | - | 表头/明细切换 |
| `table2D` | `boolean \| DataGridTable2DConfig` | - | 二维表模式 |
| `lineNo` | `boolean \| DataGridLineNoConfig` | - | 业务行号列 |
| `jointQuery` | `boolean \| DataGridJointQueryConfig` | - | 链接穿透 |
| `onShowSelectedOnlyChange` | `(active, keys, rows) => void` | - | 查看已选变化 |
| `onActiveRowKeysChange` | `(keys, record?, index?) => void` | - | 激活行变化 |
| `onCrossEntityJointCellQuery` | `(event) => void` | - | 跨实体联合单元格穿透 |

## Operation

| 参数 | 类型 | 说明 |
|--|--|--|
| `key` | `string` | 唯一标识 |
| `text` | `ReactNode` | 文案 |
| `hidden` | `boolean \| (record, index) => boolean` | 是否隐藏 |
| `disabled` | `boolean \| (record, index) => boolean` | 是否禁用 |
| `onClick` | `(record, index) => void` | 点击回调 |
| `render` | `(record, index, operation) => ReactNode` | 自定义渲染 |

## Ref

| 方法 | 说明 |
|--|--|
| `api` | 底层 TinperGrid `GridApi`（逃生舱）|
| `reload()` | 用当前 `data` 重新刷进内部 state（**不发请求**）|
| `getData()` / `getDataSource()` | 当前数据 |
| `setDataSource(rows, options?)` | 整体替换数据，`options.generateLineNo` 控制是否重算行号（默认 `true`）|
| `appendRow(row, options?)` / `appendRows(rows, options?)` | 末尾追加 |
| `insertRow(index, row, options?)` / `insertRows(index, rows, options?)` | 指定位置插入 |
| `regenerateLineNo()` | 按当前 generateType 全量重生成行号 |
| `getSelectedRowKeys()` / `getSelectedRows()` | 已选 key/行 |
| `setSelectedRowKeys(keys)` / `setSelectedRows(rows)` | 设置选择 |
| `clearSelection()` | 清空选择 |
| `getActiveRowKeys()` / `setActiveRowKeys(keys)` / `clearActiveRowKeys()` | 激活行读写 |

> `DataGrid` 的 ref **没有** `query` / `reset` / `getQueryState` 方法。数据刷新靠调用方更新 `data`。

## 易踩坑

- **没有异步请求能力**：不要传 `request/autoLoad`，不要调 `ref.query()/reset()`。服务端分页监听 `pagination.onChange` 自取后回填 `data`。
- `rowKey` 默认 `'id'`，数据没有 `id` 时必须显式传，否则选择、激活行、卡片 key 都会异常。
- `columnDefs` 使用 `field/headerName/render(value, record, rowIndex)`，不是 `dataIndex/title/render(text, record, index)` 的旧 Table 习惯。
- `ref.reload()` 不发请求，只重刷当前 `data`；要拉新数据自己请求后 `setData`。
- 列顺序拖拽、列宽拖拽**默认关闭**（`suppressMovableColumns`/`suppressResizeColumns` 默认 `true`），需要时显式传 `false`。
- 视图模式用 `displayMode`+`cardConfig`/`kanbanConfig`，旧 `viewMode/renderCard/cardLayout/showViewModeSwitch` 已废弃。
- 卡片/看板视图的操作 `maxCount` 默认 `3`，与表格操作列默认 `5` 不同。
- `cellSelection` 默认开启多区域选择/拖拽；不需要时传 `cellSelection={false}`。
- `api` 方法依赖相应 TinperGrid 模块；直接调用底层 API 报不存在时，先确认属性是否触发了模块推导或手动传了 `modules`。

## 更多示例

`demos/` 目录提供针对性示例：

| Demo | 主题 | 关键 API |
|--|--|--|
| Demo1 | 综合能力（分页/筛选/排序/合计/选择/操作列）| `columnDefs` `pagination` `rowSelection` `operations` |
| Demo2 | 操作列折叠 | `operationColumn.maxCount` |
| Demo3 | 空状态配置 | `emptyConfig` |
| Demo4 | 树表懒加载 | `loadData` `childrenColumnName` |
| Demo5 | 二维表切换 | `table2D` |
| Demo6 | 复合单元格 | `compositeLayout` `compositeControls` |
| Demo7 | 表头/明细切换 | `sumSwitch` |
| Demo8 | 业务行号 | `lineNo` `cControlType:'lineno'` |
| Demo9 | 字段穿透/单号链接 | `jointQuery` `bJointQuery` |
| Demo10 | 卡片与看板模式 | `displayMode` `cardConfig` `kanbanConfig` |
