---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础行固定
固定顶部和底部行，滚动时这些行始终可见，常用于表头行和汇总行

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowPinnedModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowpinned';

ModuleRegistry.registerModules([RowPinnedModule]);

export default function () {
  const data = [
    { id: 'header', name: '📋 表头行', sales: '', profit: '', status: 'header' },
    { id: '1', name: '产品 A', sales: 1000, profit: 200, status: 'normal' },
    { id: '2', name: '产品 B', sales: 2000, profit: 400, status: 'normal' },
    { id: '3', name: '产品 C', sales: 1500, profit: 300, status: 'normal' },
    { id: '4', name: '产品 D', sales: 3000, profit: 600, status: 'normal' },
    { id: '5', name: '产品 E', sales: 2500, profit: 500, status: 'normal' },
    { id: '6', name: '产品 F', sales: 1800, profit: 360, status: 'normal' },
    { id: '7', name: '产品 G', sales: 2200, profit: 440, status: 'normal' },
    { id: '8', name: '产品 H', sales: 2800, profit: 560, status: 'normal' },
    { id: 'total', name: '💰 总计', sales: 17820, profit: 3560, status: 'summary' },
  ];

  const columnDefs = [
    { field: 'name', headerName: '产品名称', width: 150 },
    { field: 'sales', headerName: '销售额', width: 120 },
    { field: 'profit', headerName: '利润', width: 120 },
    { field: 'status', headerName: '状态', width: 120 },
  ];

  return (
    <div>
      <style>{`
        .row-pinned-header {
          background-color: #e6f7ff !important;
          font-weight: bold;
          border-bottom: 2px solid #1890ff !important;
        }
        .row-pinned-summary {
          background-color: #fff7e6 !important;
          font-weight: bold;
          border-top: 2px solid #fa8c16 !important;
        }
      `}</style>
      <h2>基础行固定</h2>
      <p>表头行固定在顶部，汇总行固定在底部。滚动时这些行始终可见。</p>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={400}
        rowPinned={{
          topPinnedRowKeys: ['header'],
          bottomPinnedRowKeys: ['total'],
        }}
        rowStyle={{
          getRowClass: (params) => {
            if (params.data.status === 'header') return 'row-pinned-header';
            if (params.data.status === 'summary') return 'row-pinned-summary';
            return '';
          },
        }}
      />
    </div>
  );
}
```
