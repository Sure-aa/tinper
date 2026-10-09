---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础小计
在每个分组结束后插入小计行，自动计算指定列的数值总和

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { SummaryModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/summary';
import { RowStyleModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowstyle';

ModuleRegistry.registerModules([RowStyleModule, SummaryModule]);

export default function () {
  const data = [
    { id: '1', region: '华东', product: '笔记本电脑', quantity: 10, price: 5000, amount: 50000 },
    { id: '2', region: '华东', product: '台式电脑', quantity: 5, price: 4000, amount: 20000 },
    { id: '3', region: '华东', product: '显示器', quantity: 15, price: 1500, amount: 22500 },
    { id: '4', region: '华南', product: '笔记本电脑', quantity: 8, price: 5000, amount: 40000 },
    { id: '5', region: '华南', product: '台式电脑', quantity: 6, price: 4000, amount: 24000 },
    { id: '6', region: '华南', product: '显示器', quantity: 12, price: 1500, amount: 18000 },
    { id: '7', region: '华北', product: '笔记本电脑', quantity: 12, price: 5000, amount: 60000 },
    { id: '8', region: '华北', product: '台式电脑', quantity: 7, price: 4000, amount: 28000 },
    { id: '9', region: '华北', product: '显示器', quantity: 20, price: 1500, amount: 30000 },
  ];

  const columnDefs = [
    { field: 'region', headerName: '区域', width: 120 },
    { field: 'product', headerName: '产品', width: 150 },
    { field: 'quantity', headerName: '数量', width: 100 },
    { field: 'price', headerName: '单价', width: 120 },
    { field: 'amount', headerName: '金额', width: 120 },
  ];

  return (
    <div>
      <h3>基础小计</h3>
      <p>在每个区域结束后显示小计行，自动计算数量和金额的总和</p>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={500}
        summary={{
          showSubtotal: true,
          subtotalLabelColumn: 'region',
          subtotalLabelText: '小计',
          getSubtotalPosition: (data, index) => {
            if (index === data.length - 1) return true;
            return data[index].region !== data[index + 1].region;
          },
          subtotalColumns: ['quantity', 'amount'],
          precision: 2,
        }}
      />
    </div>
  );
}
```
