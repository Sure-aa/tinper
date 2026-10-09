---
tags:
  - TinperNextPro
  - GridCompat组件
---
# Table（GridCompat）兼容表格 - 从 wui-table 迁移

## 基本使用

演示把一个使用了 `multiSelect` + `sort` + `filterColumn` + `dragColumn` 多 HOC 嵌套的旧 wui-table，迁移到 `Table`（GridCompat）。无需 HOC 嵌套，改用语义化 prop 或 `compatConfig` 即可拿到 Grid 的虚拟滚动性能。

```tsx
import React, { useMemo, useState } from 'react';
import { Table } from 'tne-tinpernextpro-fe';

interface Row {
  key: string;
  name: string;
  age: number;
  dept: string;
  email: string;
  status: '在职' | '离职';
}

const source: Row[] = Array.from({ length: 500 }, (_, i) => ({
  key: String(i + 1),
  name: `员工${i + 1}`,
  age: 22 + (i % 30),
  dept: ['研发', '产品', '设计', '运营'][i % 4],
  email: `user${i + 1}@example.com`,
  status: i % 9 === 0 ? '离职' : '在职',
}));

export default function Demo1() {
  const [selectedRowKeys, setSelectedRowKeys] = useState<React.Key[]>([]);

  const columns = useMemo(() => [
    { title: '姓名', dataIndex: 'name', key: 'name', width: 120, fixed: 'left' },
    {
      title: '年龄', dataIndex: 'age', key: 'age', width: 100,
      sorter: (a: Row, b: Row) => a.age - b.age,
      filterType: 'number', filterDropdown: 'show',
    },
    {
      title: '部门', dataIndex: 'dept', key: 'dept', width: 120,
      filterType: 'dropdown', filterDropdown: 'show',
      filterDropdownData: [
        { key: '研发', value: '研发' },
        { key: '产品', value: '产品' },
        { key: '设计', value: '设计' },
        { key: '运营', value: '运营' },
      ],
    },
    { title: '邮箱', dataIndex: 'email', key: 'email', width: 220 },
    { title: '状态', dataIndex: 'status', key: 'status', width: 100 },
  ], []);

  return (
    <div style={{ height: 440 }}>
      <Table<Row>
        fieldid="gridcompat-demo1"
        rowKey="key"
        columns={columns}
        data={source}
        height={440}
        bordered
        // —— 对应旧 multiSelect(sort(filterColumn(dragColumn(Table)))) ——
        rowSelection={{
          type: 'checkbox',
          selectedRowKeys,
          getCheckboxProps: (record: Row) => ({ disabled: record.status === '离职' }),
          onChange: keys => setSelectedRowKeys(keys),
          selections: [
            Table.SELECTION_ALL,
            Table.SELECTION_INVERT,
            Table.SELECTION_NONE,
          ],
        }}
        enableSorting          // 对应 sort(Table)
        enableFilter           // 对应 filterColumn / singleFilter
        enableColumnSet        // 对应 filterColumn 的列设置部分
        draggable              // 对应 dragColumn(Table)
        dragborder             // 列宽可拖拽
        pagination={{ current: 1, pageSize: 50, total: source.length, showSizeChanger: true }}
        onChange={(p, filters, sorter, extra) => console.log(extra.action, p, sorter)}
      />
    </div>
  );
}
```

### 等价写法：用 `compatConfig` 声明原 HOC

若旧代码是 `multiSelect(sort(filterColumn(dragColumn(Table))))` 这种深嵌套，也可用 `compatConfig` 等价表达：

```tsx
<Table
  rowSelection={{ type: 'checkbox', /* ... */ }}
  compatConfig={{ multiSelect: true, sort: true, filterColumn: true, dragColumn: true }}
  // 其余不变
/>
```

两种写法等价，**新写代码推荐语义化 prop（上例）**，仅当从 HOC 嵌套代码迁移时才用 `compatConfig`。

### Demo1 还覆盖的能力（源 `demo/Demo1.js`）

组件源码的 `demo/Demo1.js` 是一个带控制面板的综合测试 demo，额外演示了：

- **树形表格**：`isTree` + `expandable` 全套（展开图标、异步 `loadData`）
- **合并单元格**：`render` 返回 `{ children, props: { rowSpan, colSpan } }`
- **行固定**：`rowPinned`（顶部 / 底部固定行）
- **右键菜单**：`popMenu` + `onPopMenuClick`
- **小计 / 合计**：Grid 风格 `summary` 与 wui-table 风格 `showSum` + 列级 `sumCol` 对照
- **多级表头**：`columns[].children` 嵌套 + `headerDisplayInRow`
- **列设置弹窗**：`enableColumnSet` + `lockable` + `columnSetOptions`

> 提示：虚拟滚动需确定高度，示例均用固定 `height` 或外层定高容器包裹。
