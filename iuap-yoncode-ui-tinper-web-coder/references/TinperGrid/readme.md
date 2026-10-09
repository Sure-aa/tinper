---
tags:
  - TinperNextPro
  - TinperGrid组件
---

# TinperGrid 表格

<!--TinperGrid-->
`TinperGrid` 是 `tne-tinpernextpro-fe/TinperGrid` 暴露的底层 `@tinper/grid` 原生入口。它提供 `Grid`、类型、`ModuleRegistry`、`AllModules` 和各功能模块；不包含 `DataGrid` 的请求/工具栏/操作列/卡片视图，也不包含 `EditGrid` 的业务编辑状态、增删行、校验和变更追踪。

## AI 使用原则

- 用户明确说“底层 Grid / TinperGrid / @tinper/grid / 手动注册模块 / 原生 API”：用 `TinperGrid`。
- 新建普通业务列表、搜索、请求分页、操作列、跨页选择：优先 `DataGrid`，不是直接 `TinperGrid`。
- 新建行内编辑、子表明细、增删行、校验、自动增行：优先 `EditGrid`，不是直接 `TinperGrid` 的 `EditModule`。
- 修改已有 `TinperGrid` 时保持底层写法，不主动替换为 `DataGrid/EditGrid`。
- 直接使用 `TinperGrid` 时必须处理模块注册；不要假设功能模块默认存在。

## 快速使用

```tsx
import React, { useMemo, useRef } from 'react';
import { Grid, GridRef, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';
import { RowSelectionModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';
import { PaginationModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/pagination';
import { ColumnSortModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/columnsort';
import { FilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/filter';
import { TextFilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/textfilter';
import type { ColumnDef } from 'tne-tinpernextpro-fe/TinperGrid';

ModuleRegistry.registerModules([
  RowNumbersModule,
  RowSelectionModule,
  PaginationModule,
  ColumnSortModule,
  FilterModule,
  TextFilterModule,
]);

export default function BasicGrid() {
  const gridRef = useRef<GridRef>(null);

  const columnDefs = useMemo<ColumnDef[]>(() => [
    { field: 'code', headerName: '编码', width: 140, sortable: true, pinned: 'left' },
    { field: 'name', headerName: '名称', width: 180, filter: 'textFilter' },
    { field: 'amount', headerName: '金额', width: 120, align: 'right' },
  ], []);

  return (
    <Grid
      ref={gridRef}
      rowKey="id"
      data={data}
      columnDefs={columnDefs}
      width={900}
      height={420}
      showRowNum={{ width: 58, pinned: 'left' }}
      rowSelection={{ mode: 'multiRow', showSelectedFilter: true }}
      pagination={{ defaultCurrent: 1, defaultPageSize: 20, showSizeChanger: true }}
      enableSorting
      enableFilter
      onReady={api => console.log(api.getPageInfo?.())}
    />
  );
}
```

## 导入路径

```tsx
// 底层 Grid 入口
import { Grid, ModuleRegistry, type GridRef, type ColumnDef } from 'tne-tinpernextpro-fe/TinperGrid';

// 默认导出也是 Grid
import Grid from 'tne-tinpernextpro-fe/TinperGrid';

// 按需模块
import { PaginationModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/pagination';
import { RowSelectionModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';

// 全模块，不推荐默认使用
import { AllModules } from 'tne-tinpernextpro-fe/TinperGrid';
```

`tne-tinpernextpro-fe` 主入口只导出 Pro 业务组件；底层 Grid 从 `tne-tinpernextpro-fe/TinperGrid` 入口取。模块联邦/TNS 场景需要确保加载 `providerEntry="TinperGrid"`。

## 模块注册

底层 Grid 的高级能力由模块提供。没有注册对应模块时，属性可能无效，`api` 方法也可能不存在。

两种注册方式：

```tsx
// 方式 1：全局注册，demo 常用；同一个 bundle 注册一次即可
ModuleRegistry.registerModules([PaginationModule, RowSelectionModule]);

// 方式 2：实例级注册，适合局部控制
<Grid modules={[PaginationModule, RowSelectionModule]} />
```

不要默认注册 `AllModules`，除非用户明确接受包体积成本或是在调试/原型阶段。业务代码优先按需注册。

## 常用模块速查

| 能力 | 模块 | 关键属性/API |
|--|--|--|
| 分页 | `PaginationModule` | `pagination`、`api.nextPage()`、`api.setPage()`、`api.getPageInfo()` |
| 行选择 | `RowSelectionModule` | `rowSelection`、`api.selectRow()`、`api.deselectAll()`、`api.getSelectedKeys()` |
| 行号 | `RowNumbersModule` | `showRowNum` |
| 行样式/激活 | `RowStyleModule` | `rowStyle`、`getCellClassName`、`api.setActiveRow()` |
| 行 hover | `RowHoverModule` | `rowHover` |
| 行固定 | `RowPinnedModule` | `rowPinned`、`api.pinRowsToTop()` |
| 行拖拽 | `RowDragModule` | `rowDrag` |
| 单元格框选/右键 | `CellSelectionModule` | `cellSelection`、`popMenu`、`onSelectionChange` |
| 列固定 | `ColumnPinnedModule` | 列 `pinned`、`enablePinned`、`api.setColumnPinned()` |
| 列设置 | `ColumnSetModule` | `enableColumnSet`、`columnSetOptions`、`api.openColumnSet()` |
| 列排序 | `ColumnSortModule` | `enableSorting`、列 `sortable`、`api.setSortModel()` |
| 列查找 | `ColumnFindModule` | `enableFind`、`api.searchColumnFind()` |
| 列宽 | `ColumnAutoSizeModule` | `dragborder`、`suppressResizeColumns`、`api.autoSizeColumns()` |
| 通用过滤 | `FilterModule` | `enableFilter`、`filter` |
| 文本/数字/日期/集合过滤 | `TextFilterModule`、`NumberFilterModule`、`DateFilterModule`、`SetFilterModule` | 列 `filter: 'textFilter'/'numberFilter'/'dateFilter'/'setFilter'` |
| 多条件/自定义过滤 | `MultiFilterModule`、`CustomFilterModule` | 列 `filter: 'multiFilter'/'customFilter'` |
| 合计/小计 | `SummaryModule` | `summary`、`api.getTotalRow()`、`isSummaryRow` |
| 树表/展开行 | `TreeModule` | `treeData`、`childrenColumnName`、`expandedRowRender`、`api.expandAll()` |
| 合并单元格 | `MergeCellsModule` | `openMergeCell`、`autoMerge`、列 `autoMergeColumn/rowSpan/colSpan` |
| 底层编辑 | `EditModule` | 列 `editable/editor/editorParams/validator`、`api.commitAllEdits()` |

## 常见功能模板

### 服务端分页

```tsx
const [page, setPage] = useState({ current: 1, pageSize: 20 });
const [data, setData] = useState([]);
const [total, setTotal] = useState(0);

<Grid
  rowKey="id"
  data={data}
  columnDefs={columnDefs}
  pagination={{
    current: page.current,
    pageSize: page.pageSize,
    total,
    showSizeChanger: true,
    onChange: async (current, pageSize) => {
      setPage({ current, pageSize });
      const result = await fetchPage({ current, pageSize });
      setData(result.list);
      setTotal(result.total);
    },
    onPageSizeChange: async (_current, pageSize) => {
      setPage({ current: 1, pageSize });
      const result = await fetchPage({ current: 1, pageSize });
      setData(result.list);
      setTotal(result.total);
    },
  }}
/>
```

如果需要业务封装（操作列、查看已选、表格/卡片/看板视图、表头明细切换等），用 `DataGrid`/`EditGrid`；注意它们同样是 `data` 驱动、**不内置异步请求**，服务端分页仍需调用方自行处理。

### 行选择

```tsx
<Grid
  rowKey="id"
  rowSelection={{
    mode: 'multiRow',
    selectedRowKeys,
    showSelectedFilter: true,
    onChange: event => setSelectedRowKeys(event.selectedKeys || []),
  }}
/>
```

不同 demo/版本里 `onChange` 参数可能出现 `(event)` 或 `(keys, rows)` 写法。为少踩坑，业务代码优先读取 `event.selectedKeys/event.selectedRows`；如果接入项目已有类型提示，以项目类型为准。

### 树表

```tsx
<Grid
  rowKey="id"
  data={treeData}
  columnDefs={columnDefs}
  treeData
  childrenColumnName="children"
  expandIconColumnIndex={0}
  defaultExpandedRowKeys={['root']}
  expandRowByClick
/>
```

### 合并单元格

```tsx
<Grid
  rowKey="id"
  data={data}
  columnDefs={[
    { field: 'department', headerName: '部门', autoMergeColumn: true },
    { field: 'team', headerName: '团队', autoMergeColumn: true },
  ]}
  openMergeCell
  autoMerge
  mergeCellAlign={{ horizontal: 'center', vertical: 'middle' }}
/>
```

### 底层编辑

```tsx
<Grid
  ref={gridRef}
  rowKey="id"
  data={data}
  columnDefs={[
    { field: 'name', headerName: '姓名', editable: true, editor: 'text' },
    { field: 'qty', headerName: '数量', editable: true, editor: 'number' },
  ]}
  onEditCommit={async edits => {
    console.log(edits);
    return true;
  }}
/>
```

底层 `EditModule` 只负责单元格编辑和提交 API，不负责新增/删除/保存取消操作列/校验错误管理/变更分类。业务编辑表格优先 `EditGrid`。

## API

### 基础配置

| 配置项 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `modules` | `Module[]` | - | 实例级模块注册 |
| `customComponents` | `ComponentRegistry` | - | 自定义组件覆盖 |
| `locale` | `GridLocale` | `zhCN` | 国际化 |
| `cacheId` | `string` | - | 列状态缓存唯一标识 |
| `fieldid` | `string` | - | 自动化标识 |
| `isRTL` | `boolean` | `false` | RTL 布局 |
| `rowKey` | `string \| ((record) => string)` | `'key'` | 行唯一标识 |

### 数据与列

| 配置项 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `data` | `any[]` | - | 数据源 |
| `dataVersion` | `number` | - | 数据版本号，强制刷新 |
| `columnDefs` | `ColumnDef[] \| ColumnGroupDef[]` | - | 列定义 |
| `defaultColDef` | `Partial<ColumnDef>` | - | 默认列配置 |
| `defaultColGroupDef` | `Partial<ColumnGroupDef>` | - | 默认列组配置 |
| `pagination` | `false \| PaginationConfig` | `false` | 分页 |
| `loading` | `boolean \| LoadingConfig` | `false` | 加载状态 |
| `showSkeleton` | `boolean` | `true` | loading 时骨架屏 |
| `emptyText` | `() => ReactNode` | - | 空状态 |
| `summary` | `false \| SummaryConfig` | `false` | 小计合计 |
| `expandedRowKeys` | `Key[]` | - | 受控展开行 |
| `defaultExpandedRowKeys` | `Key[]` | - | 默认展开行 |
| `defaultExpandAllRows` | `boolean` | `false` | 默认展开全部 |
| `expandedRowRender` | `(record, index, indent, expanded) => ReactNode` | - | 展开行内容 |

### 尺寸与显示

| 配置项 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `width` | `number` | 自动填充 | 表格宽度 |
| `height` | `number` | 按数据量计算 | 表格高度 |
| `maxHeight` | `number` | - | 最大高度 |
| `rowHeight` | `number` | `35` | 行高 |
| `headerHeight` | `number` | `30` | 表头高 |
| `fillSpace` | `boolean` | `false` | 填满父容器剩余空间 |
| `autoRowHeight` | `boolean \| AutoRowHeightConfig` | `false` | 自适应行高 |
| `textWrap` | `boolean \| TextWrapConfig` | `false` | 文本换行 |
| `showHeader` | `boolean` | `true` | 显示表头 |
| `stripeLine` | `boolean` | - | 斑马纹 |
| `showRowNum` | `boolean \| ShowRowNumConfig` | `false` | 行号 |
| `className` | `string` | - | 类名 |
| `style` | `CSSProperties` | - | 样式 |
| `rowClassNameGetter` | `(rowData, rowIndex) => string` | - | 行类名 |

### 行、列、单元格

| 配置项 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `rowSelection` | `false \| RowSelectionConfig` | `false` | 行选择 |
| `rowStyle` | `false \| RowStyleConfig` | `false` | 行样式 |
| `rowHover` | `false \| RowHoverConfig` | `false` | 行悬浮 |
| `rowPinned` | `false \| RowPinnedConfig` | `false` | 行固定 |
| `rowDrag` | `false \| RowDragConfig` | `false` | 行拖拽 |
| `cellSelection` | `false \| CellSelectionConfig` | `false` | 单元格框选 |
| `openMergeCell` | `boolean` | `false` | 合并单元格总开关 |
| `autoMerge` | `boolean` | `false` | 自动合并 |
| `edit` | `false \| EditConfig` | `false` | 单元格编辑 |
| `columnDrag` | `boolean` | `false` | 列拖拽排序 |
| `dragborder` | `boolean` | `false` | 拖拽调整列宽 |
| `suppressResizeColumns` | `boolean` | - | 列宽调整能力 |
| `enableSorting` | `boolean` | `false` | 排序总开关 |
| `enableFilter` | `boolean` | `false` | 筛选总开关 |
| `enableFind` | `boolean` | `false` | 查找总开关 |
| `enableColumnSet` | `boolean` | `false` | 列设置总开关 |
| `enablePinned` | `boolean` | `false` | 列固定总开关 |
| `columnSetOptions` | `ColumnSetConfig` | - | 列设置配置 |
| `popMenu` | `(rowKeys, colKeys) => MenuItem[]` | - | 右键菜单 |
| `onPopMenuClick` | `(type, rowKeys, colKeys) => void` | - | 右键点击 |

### 过滤和树表

| 配置项 | 类型 | 默认值 | 说明 |
|--|--|--|--|
| `filter` | `false \| FilterConfig` | `false` | 通用过滤 |
| `textFilter` | `false \| TextFilterConfig` | `false` | 文本过滤 |
| `numberFilter` | `false \| NumberFilterConfig` | `false` | 数字过滤 |
| `dateFilter` | `false \| DateFilterConfig` | `false` | 日期过滤 |
| `setFilter` | `false \| SetFilterConfig` | `false` | 集合过滤 |
| `multiFilter` | `false \| MultiFilterConfig` | `false` | 多条件过滤 |
| `treeData` | `boolean` | `false` | 树数据 |
| `childrenColumnName` | `string` | `'children'` | 子节点字段 |
| `expandAll` | `boolean` | - | 默认展开全部 |
| `expandLevel` | `number` | - | 默认展开层级 |
| `lazyLoad` | `boolean` | `false` | 懒加载子节点 |

## 事件与 Ref

```tsx
const gridRef = useRef<GridRef>(null);

<Grid
  ref={gridRef}
  onReady={api => {
    api.selectAll?.();
  }}
/>
```

| 事件 | 说明 |
|--|--|
| `onReady(api)` | Grid API 就绪 |
| `onRowClick(e, { rowIndex, rowKey, rowData })` | 行点击 |
| `onRowDoubleClick(e, context)` | 行双击 |
| `onScrollStart(scrollX, scrollY, firstRowIndex, endRowIndex)` | 滚动开始 |
| `onScrollEnd(scrollX, scrollY, firstRowIndex, endRowIndex)` | 滚动结束 |
| `onDisplayDataChange(displayData)` | 展示数据变化；不要在这里同步更新 `data` 造成循环 |
| `onSelectionChange(event, rowKeys, columnKeys)` | 框选变化 |
| `onColumnResizeEndCallback(width, columnKey)` | 列宽调整结束 |
| `onColumnReorderEndCallback(columnBefore, columnAfter, reorderColumn)` | 列拖拽结束 |

| API 分类 | 关键方法 | 所需模块 |
|--|--|--|
| 分页 | `nextPage`、`prevPage`、`setPage`、`setPageSize`、`getPageInfo` | `PaginationModule` |
| 行选择 | `selectRow`、`selectAll`、`deselectAll`、`getSelectedKeys`、`getSelectedRowsData` | `RowSelectionModule` |
| 列 | `setColumnVisible`、`setColumnWidth`、`autoSizeColumns`、`sizeColumnsToFit` | 视能力注册列模块 |
| 排序 | `setSortModel`、`sortColumn`、`clearAllSorts` | `ColumnSortModule` |
| 固定列 | `setColumnPinned`、`setColumnsPinned`、`getPinnedColumns` | `ColumnPinnedModule` |
| 列设置 | `openColumnSet`、`getColumnSetState`、`applyColumnSetState` | `ColumnSetModule` |
| 查找 | `searchColumnFind`、`findNext`、`findPrevious` | `ColumnFindModule` |
| 行固定 | `pinRowsToTop`、`pinRowsToBottom`、`clearAllPinnedRows` | `RowPinnedModule` |
| 行样式 | `setActiveRow`、`getActiveRowKey`、`refreshRowStyles` | `RowStyleModule` |
| 过滤 | `openFilter`、`applyFilters`、`clearFilter`、`setTextFilter` 等 | `FilterModule` 及具体过滤模块 |
| 合计 | `getSubtotalRows`、`getTotalRow`、`isSummaryRow`、`setSubtotalPinned` | `SummaryModule` |
| 树形 | `expandNode`、`collapseNode`、`expandAll`、`collapseAll`、`loadTreeChildren` | `TreeModule` |
| 编辑 | `startEdit`、`commitEdit`、`cancelEdit`、`getPendingEdits`、`commitAllEdits` | `EditModule` |

## Demo 路由

需要更完整示例时读取对应 demo：

| 需求 | 文件 |
|--|--|
| 自适应行高、行样式、行 hover | `references/TinperGrid/demos/Demo1.md` |
| 基础表格/行号 | `Demo2.md`、`Demo3.md` |
| 单元格框选、右键菜单 | `Demo4.md` |
| 列设置、列固定 | `Demo5.md`、`Demo6.md` |
| 底层编辑 | `Demo7.md` |
| 行选择 | `Demo8.md` |
| 分页 | `Demo9.md` |
| 树表 | `Demo10.md` |
| 展开行 | `Demo11.md` |
| 行拖拽 | `Demo12.md` |
| 合计/小计 | `Demo13.md` |
| 行样式 | `Demo14.md`、`Demo17.md` |
| 固定行 | `Demo15.md` |
| 空状态/loading | `Demo16.md` |
| 合并单元格 | `Demo18.md` |
| 行号高级配置 | `Demo19.md` |

## 易踩坑

- 直接用底层 `Grid` 时没有自动模块推导；忘记注册模块是功能不生效的首要原因。
- `AllModules` 可用但不推荐默认使用；业务页面按需注册模块，减少包体积。
- `rowKey` 默认是 `'key'`。业务数据常见字段是 `id`，务必显式传 `rowKey="id"`。
- `columnDefs` 使用 `field/headerName`，不是 `columns/dataIndex/title`。
- `render` 常见签名是 `(value, record, rowIndex) => ReactNode`；不要直接按 antd Table 的第四参数写业务逻辑。
- `onDisplayDataChange` 是展示数据变化通知，不适合在里面 `setData(displayData)`，容易形成循环或覆盖源数据。
- 服务端分页需要自己维护 `data/current/pageSize/total`；想要内置请求状态和 `query/reset` 用 `DataGrid`。
- 底层 `EditModule` 不等于 `EditGrid`。需要新增、删除、保存/取消、校验错误、变更追踪时用 `EditGrid`。
- 列 `filter: true` 通常只会触发基础文本过滤；数字/日期/集合筛选建议明确写 `numberFilter/dateFilter/setFilter` 并注册对应模块。
- 行选择 `onChange` 在不同版本/demo 中参数形态可能不同；优先按当前项目类型提示适配。
