---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 列宽策略
展示显式指定列宽与未指定列宽（默认100px）时表格的宽度计算行为

```jsx
import React, { useMemo } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([RowNumbersModule]);

const data = Array.from({ length: 10 }, (_, i) => ({
  id: i + 1,
  name: `用户 ${i + 1}`,
  age: 18 + (i % 60),
  email: `user${i + 1}@example.com`,
  address: `地址 ${i + 1}`,
}));

// 显式指定列宽：60 + 120 + 80 + 200 + 150 = 610px
const columnDefsWithWidth = [
  { field: 'id', headerName: 'ID', width: 60 },
  { field: 'name', headerName: '姓名', width: 120 },
  { field: 'age', headerName: '年龄', width: 80 },
  { field: 'email', headerName: '邮箱', width: 200 },
  { field: 'address', headerName: '地址', width: 150 },
];

// 未指定列宽：默认 100px × 5 = 500px
const columnDefsWithoutWidth = [
  { field: 'id', headerName: 'ID' },
  { field: 'name', headerName: '姓名' },
  { field: 'age', headerName: '年龄' },
  { field: 'email', headerName: '邮箱' },
  { field: 'address', headerName: '地址' },
];

export default function() {
  return (
    <div style={{ padding: '20px' }}>
      <div style={{ marginBottom: '24px' }}>
        <h4>1. 显式指定列宽（总宽 610px）</h4>
        <Grid data={data} columnDefs={columnDefsWithWidth} rowKey="id" showRowNum={true} fillSpace={false} />
      </div>
      <div>
        <h4>2. 未指定列宽（默认 100px × 5 = 500px）</h4>
        <Grid data={data} columnDefs={columnDefsWithoutWidth} rowKey="id" showRowNum={true} fillSpace={false} />
      </div>
      <p style={{ marginTop: 16, fontSize: 14, color: '#666' }}>
        未指定 width 且 fillSpace=false 时，表格根据列宽自动计算总宽度，未设宽度的列默认 100px。
      </p>
    </div>
  );
}
```
