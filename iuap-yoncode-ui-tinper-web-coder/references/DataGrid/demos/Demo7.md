---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 表头/明细切换

## 基本使用

`sumSwitch` 在「只看表头（主表）」与「表头 + 明细」之间切换；切换时可用不同 `rowKey` 并清空已选。

```tsx
import React, { useState } from 'react';
import { DataGrid } from 'tne-tinpernextpro-fe';

// 每行同时带 id（表头模式）和 detailKey（明细模式）
const data = [
  {
    id: '1', detailKey: '1-detail', code: 'SO-001', customer: '用友网络', amount: 12000,
    details: [{ product: '机器人底座', quantity: 12 }, { product: '视觉相机', quantity: 8 }],
  },
  {
    id: '2', detailKey: '2-detail', code: 'SO-002', customer: '星河制造', amount: 8600,
    details: [{ product: '包装箱', quantity: 180 }],
  },
];

const columnDefs = [
  { field: 'code', headerName: '订单编号', width: 150, pinned: 'left' },
  { field: 'customer', headerName: '客户', width: 160 },
  {
    field: 'detailSummary', headerName: '明细摘要', width: 300,
    cControlType: 'composite',
    cExtProps: {
      crossEntity: 'details',
      compositeControls: { controls: [{ cItemName: 'product' }, { cItemName: 'quantity' }] },
    },
  },
];

export default function Demo7() {
  const [selectedRowKeys, setSelectedRowKeys] = useState<React.Key[]>([]);

  return (
    <DataGrid
      rowKey="id"
      data={data}
      columnDefs={columnDefs as any}
      pagination={false}
      rowHeight={82}
      height={360}
      width={1120}
      rowSelection={{
        mode: 'multiRow', selectedRowKeys,
        onChange: e => setSelectedRowKeys(e.selectedKeys),
      }}
      sumSwitch={{
        defaultValue: true,          // true=只看表头，false=表头+明细
        keys: { true: 'id', false: 'detailKey' },  // 两种模式用不同 rowKey
        onChange: (value, ctx) => {
          setSelectedRowKeys([]);    // 切换时清空已选
          console.log(`切换为${value ? '表头' : '表头+明细'}，rowKey=${ctx.rowKey}`);
        },
      }}
    />
  );
}
```

> `defaultValue=true` 为表头模式（隐藏明细列）；`keys.true`/`keys.false` 指定两种模式的 rowKey 字段；切换通过 `onChange(value, context)` 通知外部，context 含 `rowKey`/`selectedRowKeys`。
