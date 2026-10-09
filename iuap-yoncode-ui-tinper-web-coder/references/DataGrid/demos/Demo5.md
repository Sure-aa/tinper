---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 二维表切换

## 基本使用

`table2D` 把一维明细切换为「行维度 × 列维度」的交叉录入矩阵，在二维表修改交叉点后通过 `onCellChange` 回写一维数据。

```tsx
import React, { useState } from 'react';
import { DataGrid } from 'tne-tinpernextpro-fe';

const initialData = [
  { id: '1', product: '产品A', period: '2026-Q1', quantity: 100, amount: 10000, price: 100 },
  { id: '2', product: '产品A', period: '2026-Q2', quantity: 120, amount: 13200, price: 110 },
  { id: '3', product: '产品B', period: '2026-Q1', quantity: 80, amount: 9600, price: 120 },
  { id: '4', product: '产品B', period: '2026-Q2', quantity: 90, amount: 11700, price: 130 },
];

export default function Demo5() {
  const [data, setData] = useState(initialData);

  return (
    <DataGrid
      rowKey="id"
      data={data}
      columnDefs={[
        { field: 'product', headerName: '产品', width: 140, pinned: 'left' },
        { field: 'period', headerName: '期间', width: 120 },
        { field: 'quantity', headerName: '数量', width: 110, align: 'right', fieldType: 'number' },
        { field: 'amount', headerName: '金额', width: 120, align: 'right', fieldType: 'number' },
        { field: 'price', headerName: '均价', width: 110, align: 'right', fieldType: 'number' },
      ]}
      pagination={false}
      table2D={{
        defaultShow2D: true,
        switchOptions: [{ value: false, text: '一维表' }, { value: true, text: '二维表' }],
        rowFields: ['product'],       // 行维度
        columnFields: ['period'],     // 列维度
        crossFields: ['quantity', 'amount'],  // 交叉点度量（展开到单元格）
        measureFields: ['price'],     // 附加展示列，不参与交叉
        subtotalText: '小计',
        totalText: '合计',
        onCellChange: ctx => setData(ctx.nextData),  // 二维修改回写一维数据
      }}
      height={360}
      width={980}
    />
  );
}
```

> `rowFields` 行维度、`columnFields` 列维度、`crossFields` 交叉点度量、`measureFields` 附加度量列。修改交叉单元格经 `onCellChange` 的 `ctx.nextData`（已回写源行）更新一维数据，`ctx` 还含 `sourceRowIndex`/`sourceField`/`value` 等。
