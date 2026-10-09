---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础行样式
使用 rowClass 为行添加统一样式，支持通过 getRowClass 动态设置不同行的样式

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowStyleModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowstyle';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([RowStyleModule, RowNumbersModule]);

export default function () {
  const data = Array.from({ length: 20 }, (_, i) => ({
    id: String(i + 1),
    name: `产品 ${i + 1}`,
    price: (Math.random() * 1000).toFixed(2),
    stock: Math.floor(Math.random() * 100),
    category: ['电子产品', '服装', '食品', '图书'][i % 4],
  }));

  const columnDefs = [
    { field: 'name', headerName: '产品名称', width: 150 },
    { field: 'price', headerName: '价格', width: 100 },
    { field: 'stock', headerName: '库存', width: 100 },
    { field: 'category', headerName: '类别', width: 120 },
  ];

  return (
    <div>
      <style>{`
        .extend_row-highlight,
        .extend_row-highlight .public_fixedDataTableCell_main {
          background-color: #f0f5ff !important;
        }
        .extend_row-highlight:hover {
          background-color: #f0f5ff !important;
        }
      `}</style>
      <h2>基础行样式</h2>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={400}
        showRowNum={true}
        rowStyle={{ rowClass: 'row-highlight' }}
      />
    </div>
  );
}
```
