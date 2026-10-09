---
tags:
  - TinperNextPro
  - GridCompat组件
---

# Table（GridCompat）兼容表格

<!--GridCompat-->
`Table`（内部实现为 `GridCompat`）是 TinperNextPro 提供的**表格迁移 / 兼容组件**：内部直接渲染 `@tinper/grid` 的高性能 Grid，外层加一层适配器，把 `@tinper/next-ui` 的 `Table`（wui-table，含 `multiSelect` / `sort` / `filterColumn` / `dragColumn` / `sum` / `bigData` 等 HOC 体系）的 API **翻译成 Grid 的原生 API**。

> 它的存在目的是**让使用旧 wui-table 的存量代码低成本的迁移到 Grid 的虚拟滚动性能**，不是给新项目用的主力表格。新项目请直接用 `DataGrid` / `EditGrid`（见下文「AI 使用原则」）。

## ⚠️ 命名辨析：两个 `Table` 不要搞混

| 来源 | 导入写法 | 是什么 |
|------|----------|--------|
| **TinperNextPro** | `import { Table } from 'tne-tinpernextpro-fe'` | 本文档：Grid 渲染 + wui-table API 兼容层（**迁移用**） |
| **@tinper/next-ui** | `import { Table } from '@tinper/next-ui'` | 基础 DOM 表格 wui-table（`references/wui-table/api.md`） |

两者 API 高度相似（本就是为兼容它），但**渲染内核不同**：前者是 Canvas/虚拟滚动的 Grid，后者是传统 DOM 表格。导入时务必确认来源包。

## AI 使用原则

- **存量迁移**：原代码用的是 `@tinper/next-ui` 的 `Table` + HOC（`multiSelect` / `sort` / `filterColumn` / `dragColumn` / `sum` …），只想拿到 Grid 性能、不愿大规模重写 —— 这是 `Table`（GridCompat）的**唯一目标场景**。
- **新建表格**：不要用 `Table`（GridCompat），直接选 `DataGrid`（列表/分页/业务表格）或 `EditGrid`（行内编辑/子表）。选型先走 `../rules/selection-rules.md` 决策 0。
- **改动项目已有表格**：保持原组件不替换。GridCompat 是「想从 wui-table 迁到 Grid」的过渡选择，不是「已有 DataTable/DataGrid 要替换」的选择。
- 不要把 `DataGrid` 的 `columnDefs/field` 套给 `Table`；`Table` 沿用 wui-table 的 `columns/dataIndex` 体系。

## 快速使用

```tsx
import React, { useMemo, useState } from 'react';
import { Table } from 'tne-tinpernextpro-fe';
import type { CompatColumnType } from 'tne-tinpernextpro-fe';

interface OrderRow {
  key: string;
  code: string;
  customer: string;
  amount: number;
  status: string;
}

const data: OrderRow[] = Array.from({ length: 200 }, (_, i) => ({
  key: String(i + 1),
  code: `SO-${String(i + 1).padStart(4, '0')}`,
  customer: ['华北', '华东', '华南'][i % 3],
  amount: 1000 + i * 37,
  status: i % 4 === 0 ? '已关闭' : '进行中',
}));

export default function OrderTable() {
  const [selectedRowKeys, setSelectedRowKeys] = useState<React.Key[]>([]);

  const columns = useMemo<CompatColumnType<OrderRow>[]>(() => [
    { title: '单据编号', dataIndex: 'code', key: 'code', width: 140, fixed: 'left' },
    { title: '客户', dataIndex: 'customer', key: 'customer', width: 120 },
    {
      title: '金额', dataIndex: 'amount', key: 'amount', width: 120, align: 'right',
      sorter: (a, b) => a.amount - b.amount,   // 列写 sorter 即可排序
    },
    { title: '状态', dataIndex: 'status', key: 'status', width: 120 },
  ], []);

  return (
    // 虚拟滚动需要确定高度：用 height 或父容器定高 + fillSpace
    <div style={{ height: 420 }}>
      <Table<OrderRow>
        fieldid="order-table"
        rowKey="key"
        columns={columns}
        data={data}
        bordered
        height={420}
        enableSorting                 // 启用排序（也可在列上写 sorter 自动启用）
        pagination={{
          current: 1, pageSize: 20, total: data.length,
          showTotal: (t, r) => `${r[0]}-${r[1]} 共 ${t} 条`,
        }}
        rowSelection={{
          type: 'checkbox',
          selectedRowKeys,
          onChange: keys => setSelectedRowKeys(keys),
        }}
        onChange={(p) => console.log('分页/排序/筛选变化', p)}
      />
    </div>
  );
}
```

## 本质与定位

`GridCompat` 内部只有一句核心渲染：

```tsx
<Grid ref={gridRef} {...computedGridProps} modules={modules} locale={gridLocale} />
```

即「`@tinper/grid` 的 `Grid` + 一层 wui-table API 翻译器」。它解决的是：Grid 性能强但 API 与 wui-table 完全不同，存量项目逐行重写成本高。改个 import、声明一下原 HOC，就能拿到 Grid 的虚拟滚动。

| 组件 | 渲染内核 | API 风格 | 定位 |
|------|----------|----------|------|
| `@tinper/grid` `Grid` / `TinperGrid` | Canvas 虚拟滚动 | 原生 Grid API（`columnDefs`） | 最底层 |
| `DataGrid` / `EditGrid` | Canvas 虚拟滚动 | 原生 Grid API + 业务封装 | **新建首选** |
| **`Table`（GridCompat）** | Canvas 虚拟滚动 | **wui-table API**（`columns`/HOC） | **存量迁移** |
| `@tinper/next-ui` `Table`（wui-table） | 传统 DOM | wui-table API（`columns`/HOC） | 兼容目标 |
| `DataTable` / `EditTable` | 基于 wui-table | wui-table API + 业务封装 | 旧业务表格 |

> 多一层适配就有多一层开销（虽小但非零），且永远落后于 Grid 原生新特性。因此**不要把 GridCompat 写进新项目**，否则等于把「翻译层」当长期依赖，后续 Grid 升级反而受适配层约束。

## 声明能力的两种方式

GridCompat 提供两套等价写法，**新写代码优先用语义化 prop，仅从 HOC 嵌套代码迁移时才用 `compatConfig`**。

### 方式 A：语义化 prop（推荐）

直接用 `rowSelection` / `enableSorting` / `enableColumnSet` / `enableFilter` 等语义化属性，无需声明 HOC：

```tsx
<Table
  rowSelection={{ type: 'checkbox', onChange }}   // 自动注册行选择
  enableSorting                                    // 自动注册排序
  enableColumnSet                                  // 自动注册列设置
  enableFilter                                     // 自动注册过滤
  pagination={{ current, pageSize }}               // 自动注册分页
/>
```

### 方式 B：compatConfig（从 HOC 迁移时用）

旧代码若用 `multiSelect(sort(Table))` 这类 HOC 嵌套，可用 `compatConfig` 声明原用了哪些 HOC，等价替换：

```tsx
<Table
  compatConfig={{
    multiSelect: true,     // 对应旧 multiSelect(Table, Checkbox)
    sort: true,            // 对应旧 sort(Table)
    filterColumn: true,    // 对应旧 filterColumn(Table)（列设置）
    dragColumn: true,      // 对应旧 dragColumn(Table)
    // bigData: true,      // 空实现，Grid 已内置虚拟滚动，无需声明
    // sum: true,          // ⚠️ 暂不支持，会被忽略；合计请用 showSum / summary
  }}
/>
```

| `compatConfig` 字段 | 对应旧 HOC | 说明 |
|---------------------|-----------|------|
| `multiSelect` | `multiSelect(Table, Checkbox)` | 多选 |
| `singleSelect` | `singleSelect(Table, Radio)` | 单选 |
| `sort` | `sort(Table)` | 排序 |
| `bigData` | `bigData(Table)` | **空实现**，Grid 已内置虚拟滚动 |
| `filterColumn` | `filterColumn(Table)` | 列设置 / 列筛选 |
| `dragColumn` | `dragColumn(Table)` | 列拖拽 |
| `sum` | `sum(Table)` | ⚠️ **暂不支持**，会被忽略 |
| `enableColumnSet` / `enableFind` | — | 列设置 / 列查找 |

旧 HOC 静态方法（`Table.multiSelect` / `Table.sort` / …）仍可用，保留兼容；新代码不必再嵌套 HOC。

## 与 @tinper/next-ui Table 的 API 兼容性

绝大多数 wui-table API 可直接复用或微调。**绝大多数列基础属性、排序、过滤、行选择、分页、单元格合并、行事件均可直接使用**，少量需要留意：

| 旧 API | 迁移注意 |
|--------|----------|
| `dataSource` | 仍支持，推荐改用 `data` |
| `scroll={{ x, y }}` | 自动转换为 `width`/`height`；`scroll.x` 为百分比字符串时适配层会用 ResizeObserver 测量。推荐直接用 `height` |
| `isSort` / `isFilterColumn` / `isDragColumn` / `isSum` | 旧开关名仍被识别；新代码推荐 `enableSorting` / `enableColumnSet` / `enableFilter` / `showSum` |
| 排序方向 `ascend/descend` | 无需改，适配层自动转 Grid 的 `asc/desc` |
| 过滤类型 `text/dropdown/date/number` | 无需改，自动映射为 Grid 的 textFilter/setFilter/dateFilter/numberFilter |
| `sumClassName` | ⚠️ 不支持（Grid 的 SummaryConfig 无样式类名） |
| `sum` (sumX) 整体能力 | ⚠️ 暂不支持，合计请用 `showSum` + 列级 `sumCol`，或 Grid 风格 `summary` |
| `onChange` 第四参数 | 多了 `extra.action`（`'sort' \| 'filter' \| 'paginate'`），原仅 3 参 |

## API

### 数据 / 基础

| 参数 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `data` | `T[]` | `[]` | 数据源（推荐） |
| `dataSource` | `T[]` | `[]` | `data` 别名 |
| `columns` | `CompatColumnType[]` | `[]` | 列定义；与 `children` 二选一，`columns` 优先 |
| `rowKey` | `string \| ((record) => string)` | `'key'` | 行唯一标识 |
| `children` | `ReactNode` | — | `<Table.Column>` 子节点声明列 |

### 尺寸 / 滚动

| 参数 | 类型 | 说明 |
|------|------|------|
| `width` / `height` | `number` | 宽/高（**虚拟滚动需给定高度**） |
| `scroll` | `{ x?, y? }` | 旧 API，自动转 width/height |
| `rowHeight` / `headerHeight` | `number` | 行高 / 表头高 |
| `size` | `'sm' \| 'md' \| 'lg'` | 紧凑/默认/宽松 |
| `fillSpace` | `boolean` | 自动填充父容器（父容器需定高） |
| `bodyDisplayInRow` / `textWrap` | `boolean` | 单元格是否换行 |

### 显示 / 样式

| 参数 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `showHeader` | `boolean` | `true` | 显示表头 |
| `bordered` | `boolean` | `false` | 边框 |
| `stripeLine` | `boolean` | `false` | 斑马纹 |
| `loading` | `boolean \| object` | `false` | 加载态 |
| `emptyText` | `ReactNode \| (() => ReactNode)` | `'暂无数据'` | 空数据提示 |
| `title` / `footer` | `ReactNode \| ((data) => ReactNode)` | — | 标题 / 页脚 |
| `showRowNum` | `boolean \| { key?, fixed?, width?, name?, base? }` | — | 行号 |
| `rowClassName` | `(record, index) => string` | — | 行类名 |

### 行选择

| 参数 | 类型 | 说明 |
|------|------|------|
| `rowSelection` | `object \| false` | 存在即自动注册选择模块，优先级高于 `compatConfig` |
| `rowSelection.type` | `'checkbox' \| 'radio'` | 选择类型 |
| `rowSelection.selectedRowKeys` / `defaultSelectedRowKeys` | `Key[]` | 受控 / 默认选中 |
| `rowSelection.onChange` | `(keys, rows, e) => void` | 选择变化 |
| `rowSelection.onSelect` | `(record, selected, rows, nativeEvent) => void` | 单选回调 |
| `rowSelection.getCheckboxProps` | `(record, index) => object` | 单行勾选属性（如禁用） |
| `rowSelection.checkStrictly` | `boolean` | 树表父子是否独立 |
| `rowSelection.selections` | `array \| boolean` | 表头自定义选择项，支持 `Table.SELECTION_ALL/INVERT/NONE` |
| `rowSelection.columnTitle/columnWidth/fixed` | — | 选择列定制 |

### 分页

| 参数 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `pagination` | `object \| false` | — | 存在即自动注册分页模块 |
| `.current` / `.defaultCurrent` | `number` | `1` | 当前页 |
| `.pageSize` / `.defaultPageSize` | `number` | `10` | 每页条数 |
| `.total` | `number` | — | 总条数 |
| `.showSizeChanger` / `.showQuickJumper` | `boolean` | `false` | 切换器 / 跳转 |
| `.onChange(page, pageSize)` | 函数 | — | 页码变化 |
| `.showTotal` | `boolean \| ((total, range) => ReactNode)` | — | 显示总数 |

### 排序 / 过滤

| 参数 | 类型 | 说明 |
|------|------|------|
| `enableSorting` / `isSort` | `boolean` | 启用排序（列写 `sorter` 也可自动启用） |
| `sort` | `{ mode: 'single' \| 'multiple', backSource?, sortFun? }` | 排序配置 |
| `sortDirections` | `('ascend' \| 'descend')[]` | 默认方向循环 |
| `showSorterTooltip` | `boolean \| object` | 排序提示 |
| `enableFilter` / `filterable` | `boolean` | 启用过滤 |
| `filterMode` | `'single' \| 'multiple'` | 默认 `'multiple'` |
| `onFilterChange(field, value, condition)` | 函数 | 过滤变化 |
| `onFilterClear(dataIndex)` | 函数 | 清除过滤 |

### 列宽 / 列拖拽 / 列设置

| 参数 | 类型 | 说明 |
|------|------|------|
| `dragborder` | `boolean \| 'default' \| 'fixed'` | 列宽可拖拽调整 |
| `draggable` | `boolean` | 列顺序可拖拽 |
| `minColumnWidth` / `maxColumnWidth` | `number` | 表格级列宽上下限 |
| `enableColumnSet` | `boolean` | 启用列设置弹窗 |
| `enableFind` | `boolean` | 启用列查找 |
| `lockable` | `boolean \| 'enable' \| 'disable' \| 'onlyHeader' \| 'onlyPop'` | 列锁定（映射到 `enablePinned`） |
| `columnSetOptions` | `object` | `{ showFooter, showSelectAll, showSelected, showColumnAutoWidth, showColumnMover, showReset, showToTop, showLock }` |

### 行拖拽 / 树形 / 展开行

| 参数 | 类型 | 说明 |
|------|------|------|
| `rowDraggAble` | `boolean \| object` | 启用行拖拽；`useDragHandle` 控制是否仅手柄可拖 |
| `onDropRow(data, record, index, dropRecord, dropIndex, e)` | 函数 | 行拖拽完成 |
| `isTree` | `boolean` | 启用树形数据 |
| `childrenColumnName` | `string` | 默认 `'children'` |
| `expandable` | `object` | 展开配置（也支持平铺属性） |
| `expandedRowRender(record, index, indent)` | 函数 | 展开行渲染 |
| `loadData(record)` | `Promise<T[]>` | 异步加载子节点 |

### 汇总 / 其它

| 参数 | 类型 | 说明 |
|------|------|------|
| `showSum` | `string[]` | 显示哪些汇总：`['subtotal']` / `['total']` / `['subtotal','total']` |
| `summary` | `object` | Grid 风格完整汇总配置（showSubtotal/showTotal、subtotal/total 列、precision、formatNumber 等） |
| `compatConfig` | `object` | 声明原 HOC（见上文） |
| `onChange(pagination, filters, sorter, extra)` | 函数 | 统一变化回调，`extra.action` ∈ `'sort'\|'filter'\|'paginate'` |
| `cacheId` | `string` | 列状态持久化 key（localStorage，不要含敏感信息） |
| `onRowClick` / `onRowDoubleClick` / `onRowHover` | 函数 | 行事件 |

## Column / ColumnGroup

`Column` 主要属性：

| 参数 | 说明 |
|------|------|
| `title` / `dataIndex` / `key` | 标题 / 数据字段 / 唯一标识 |
| `width` / `minWidth` / `maxWidth` | 列宽 |
| `fixed` | `'left' \| 'right' \| true` |
| `align` / `titleAlign` / `contentAlign` | 对齐 |
| `ellipsis` | 省略号 |
| `render(record, index, text, config)` | 自定义渲染；返回 `{ children, props: { rowSpan, colSpan } }` 可合并单元格 |
| `sorter` / `sortOrder` / `orderNum` / `sortDirections` | 排序 |
| `filterType` / `filterDropdown` / `filterDropdownData` / `onFilter` | 过滤 |
| `onCell(record, index)` | 单元格属性/事件 |
| `sumCol` / `sumPrecision` / `sumRender` / `totalRender` | 列级汇总 |
| `children` | 多级表头 |

`<Table.Column>` / `<Table.ColumnGroup>` 是**虚拟组件**（仅做 JSX 声明，本身不渲染 DOM）。`columns` prop 与 children 可共存，`columns` 优先。

## Ref

| 方法 | 说明 |
|------|------|
| `api` | 原始 `@tinper/grid` 的 `GridApi`（逃生舱，可调用所有底层方法） |
| `getSelectedRowKeys()` | 获取选中 keys |
| `getSelectedRows()` | 获取选中行数据 |
| `setSelectedRowKeys(keys)` | 设置选中 |
| `clearSelection()` | 清空选中 |

## 易踩坑

- **必须给高度**：虚拟滚动默认开启（Grid 内置），表格必须有确定高度，否则高度为 0 不显示。用 `height` 或父容器定高 + `fillSpace`。
- **排序不生效**：要么 `enableSorting` / `isSort`，要么在列上写 `sorter`，否则点表头不排序。
- **`sum` / `sumClassName` 不支持**：`compatConfig.sum` 和 `sumClassName` 会被忽略；合计用 `showSum` + 列级 `sumCol`，或 Grid 风格的 `summary`。
- **`bigData` 是空壳**：HOC `bigData` 仅为 API 兼容（Grid 已内置虚拟滚动），包了等于没包，别当开关用。
- **合并单元格自动检测可能不准**：适配层靠扫描 `render` 源码是否含 `colSpan`/`rowSpan` 决定是否注册合并模块；不准时用 `gridConfig.modules: ['mergeCells']` 显式声明。
- **`onChange` 第四参数**：相比旧 wui-table 多了 `extra.action`，注意回调签名对齐。
- **`cacheId` 持久化**：列宽/顺序/显隐会写入 localStorage（key 形如 `tinper-grid-columnDefsState-${cacheId}`），不同表格要用不同 `cacheId`，不要含敏感信息。

## 何时该迁离 GridCompat

如果已经用 `Table`（GridCompat）迁移完毕、且后续要做 Grid 独有的高级能力（如 `summary` 高级配置、`cellSelection`、`rowPinned` 等），建议逐步迁到 `DataGrid`（直接用原生 Grid API，无翻译层）。GridCompat 是过渡，不是终点。
