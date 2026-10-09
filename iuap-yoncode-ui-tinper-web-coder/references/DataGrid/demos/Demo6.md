---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 复合单元格

## 基本使用

同一单元格内用「复合控件」布局多字段：单实体用 `compositeLayout` 自定义多行多列排版；跨实体用 `compositeControls` + `crossEntity` 渲染关联子表明细。

```tsx
import React from 'react';
import { DataGrid } from 'tne-tinpernextpro-fe';

const data = [
  {
    id: '1', code: 'SO-001', customer: '用友网络', owner: '张三', amount: 12000, profit: 3000,
    details: [
      { product: '机器人底座', quantity: 12, deliveryDate: '2026-07-12' },
      { product: '视觉相机', quantity: 8, deliveryDate: '2026-07-18' },
    ],
  },
  {
    id: '2', code: 'SO-002', customer: '星河制造', owner: '李四', amount: 8600, profit: 2100,
    details: [{ product: '包装箱', quantity: 180, deliveryDate: '2026-07-25' }],
  },
];

const columnDefs = [
  { field: 'code', headerName: '订单编号', width: 150, pinned: 'left' },
  {
    field: 'orderSummary', headerName: '订单摘要（单实体）', width: 260,
    cControlType: 'composite',
    cExtProps: {
      compositeLayout: [
        { row: [{ col: [
          { cItemName: 'customer', bShowCaption: true, joinIcon: '/', style: { fontWeight: 600 } },
          { cItemName: 'owner' },
        ]}]},
        { row: [{ col: [
          { cItemName: 'amount', bShowCaption: true, joinIcon: '~' },
          { cItemName: 'profit', bShowCaption: true },
        ]}]},
      ],
    },
  },
  {
    field: 'detailSummary', headerName: '明细摘要（跨实体）', width: 300,
    cControlType: 'composite',
    cExtProps: {
      crossEntity: 'details',
      compositeControls: { controls: [
        { cItemName: 'product', bJointQuery: true },
        { cItemName: 'quantity' },
        { cItemName: 'deliveryDate' },
      ]},
    },
  },
];

export default function Demo6() {
  return (
    <DataGrid
      rowKey="id"
      data={data}
      columnDefs={columnDefs as any}
      pagination={false}
      rowHeight={82}
      height={360}
      width={1120}
      onCrossEntityJointCellQuery={e =>
        console.log('穿透：主表行', e.parentRowIndex, '子表行', e.rowIndex, '字段', e.cellName)
      }
    />
  );
}
```

> 单实体：`compositeLayout` 的 `row[].col[]` 每项用 `cItemName` 绑定本行字段，`bShowCaption` 显示字段名、`joinIcon` 连接符。跨实体：`crossEntity` 指定子数据字段（如 `details`），`compositeControls.controls` 渲染子表字段；子项 `bJointQuery:true` 可点击触发 `onCrossEntityJointCellQuery`。复合行建议加大 `rowHeight`。
