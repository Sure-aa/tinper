# Table 使用模式（来自真实项目蒸馏）

> **选型前先判断：改动已有表格 还是 新建表格**（详见 `../rules/selection-rules.md` 决策 0）。
> - 改动项目已有表格：直接在原表上改，**保持原组件类型**，不要把 `Table`/`DataTable`/`EditTable` 替换为 Grid 系列。
> - 新建表格：可编辑/子表/明细/增删行优先 **EditGrid**，基础/普通表格优先 **TinperGrid**，其余优先 **DataGrid**；仅用户明确指定才用 `Table`/`DataTable`/`EditTable`。

## 1. 新建表格时的选型（DataGrid / EditGrid / TinperGrid 优先）

| 场景（新建） | 首选 | 备选（仅用户指定） | 理由 |
|------|------|------|------|
| 列表页 + 分页 + 操作列 + 排序筛选 | DataGrid | DataTable | data 驱动 + operations/rowSelection；服务端分页由调用方在 pagination.onChange 自取 |
| 行内编辑、子表、明细表、增删行 | EditGrid | EditTable | 原生 Grid API + 编辑能力 |
| 基础/普通表格、按需引入 Grid 模块 | TinperGrid | wui-table | 直接暴露 @tinper/grid 原始 API，无业务封装 |
| 需要 HOC 灵活组合 | DataGrid | Table + HOCs | Grid 内置拖拽/排序/大数据，HOC 为旧模式回退 |

## 2. Table HOC 链式组合模式

```js
import { Table, Checkbox } from '@tinper/next-ui';
import { multiSelect, dragColumn, bigData, singleFilter, sort, sum } from '@tinper/next-ui';

const ComposedTable = dragColumn(bigData(multiSelect(Table, Checkbox)));
```

**组合顺序规则**：外层包内层，从外到内依次是：
- `dragColumn` — 列宽拖拽
- `bigData` — 大数据虚拟滚动
- `multiSelect` — 多选行（需传 Checkbox）
- `singleFilter` — 单列筛选
- `sort` — 排序
- `sum` — 合计行

## 3. 主从联动模式（Master-Detail）

```jsx
// 主表
<DataTable
  ref={masterRef}
  columns={masterColumns}
  request={fetchMasterData}
  operationTypeProps={{ rowActiveKeysMode: 'single' }}
  rowActiveKeys={activeKeys}
  onRowClick={(record) => {
    setActiveKeys([record.id]);
    detailRef.current.queryData({ params: { masterId: record.id } });
  }}
/>

// 从表
<DataTable
  ref={detailRef}
  columns={detailColumns}
  request={fetchDetailData}
/>
```

## 4. DataTable 操作列配置

```jsx
<DataTable
  operationItems={[
    { key: 'edit', text: '编辑' },
    { key: 'delete', text: '删除', otherProps: { disabled: !hasPermission } },
    { key: 'detail', text: '详情', rowActivable: true },
  ]}
  operationClick={(record, item) => {
    if (item.key === 'edit') openEditModal(record);
    if (item.key === 'delete') confirmDelete(record);
  }}
  operationType="link"
  operationTypeProps={{ maxCount: 3 }}
/>
```

## 5. rowSelection 新旧 API

**新 API（推荐）**：
```jsx
<Table
  rowSelection={{
    type: 'checkbox',
    selectedRowKeys,
    onChange: (keys, rows) => setSelectedRowKeys(keys),
  }}
/>
```

**旧 API（勿用于新项目）**：数据记录上设置 `_checked`/`_disabled` 字段 + `getSelectedDataFunc` 回调。**不要混用两套 API**。

## 6. 数据 key 规则

无论 Table/DataTable/EditTable，数据必须含唯一 key：
```jsx
<DataTable rowKey="id" data={data.map(item => ({ ...item, key: item.id }))} />
```

## 7. DataTable request 返回结构（高频踩坑）

`request` 函数接收 `{params, filters, sort}` 参数，必须返回 `Promise<{data, success?, total?}>`：

```js
const fetchData = async ({ params, filters, sort }) => {
  const res = await api.list({
    ...params,
    pageNum: params?.page?.current,
    pageSize: params?.page?.pageSize,
  });
  return { data: res.rows, success: true, total: res.total };
};

<DataTable columns={columns} request={fetchData} />
```

**注意**：
- `success` 为 `false` 或缺失时，表格不更新数据
- `total` 不返回时，表格认为是前端分页，会将 `data` 全量加载后在前端切页
- 不要返回 `dataSource`，DataTable 内部使用 `data` 字段
