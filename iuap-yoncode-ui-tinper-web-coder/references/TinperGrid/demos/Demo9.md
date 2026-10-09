---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 客户端分页
数据全量加载到内存，由组件自动分页切片，支持分页大小切换和行选择联动

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { PaginationModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/pagination';
import { RowSelectionModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([PaginationModule, RowSelectionModule, RowNumbersModule]);

export default function() {
  const data = Array.from({ length: 500 }, (_, i) => ({
    id: i + 1,
    name: `用户 ${i + 1}`,
    age: 18 + (i % 60),
    email: `user${i + 1}@example.com`,
    department: ['研发部', '产品部', '设计部', '市场部'][i % 4],
  }));

  const columnDefs = [
    { field: 'name', headerName: '姓名', width: 120 },
    { field: 'age', headerName: '年龄', width: 80 },
    { field: 'email', headerName: '邮箱', width: 200 },
    { field: 'department', headerName: '部门', width: 120 },
  ];

  return (
    <div>
      <h2>客户端分页</h2>
      <p style={{ color: '#666', marginBottom: 20 }}>数据总数: {data.length} 条，全部加载到浏览器内存，由组件自动分页切片</p>
      <Grid
        data={data}
        rowKey="id"
        columnDefs={columnDefs}
        width={800}
        height={500}
        pagination={{
          defaultCurrent: 1,
          defaultPageSize: 20,
          showSizeChanger: true,
          pageSizeOptions: [5, 10, 20, 50],
        }}
        rowSelection={{
          mode: 'multiRow',
          showSelectedFilter: true,
          onChange: (keys, rows) => console.log('选择变化:', keys, rows),
        }}
        showRowNum={true}
      />
    </div>
  );
}
```

## 服务端分页
数据按页从服务端加载，通过 onChange 回调触发数据请求，total 控制总页数

```jsx
import React, { useState, useRef } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { PaginationModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/pagination';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([PaginationModule, RowNumbersModule]);

const generateData = (count, offset = 0) =>
  Array.from({ length: count }, (_, i) => ({
    id: offset + i + 1,
    name: `商品 ${offset + i + 1}`,
    price: (100 + (offset + i) * 5).toFixed(2),
    stock: 100 + ((offset + i) % 500),
    category: ['电子产品', '图书', '服装', '食品', '家居'][(offset + i) % 5],
  }));

export default function () {
  const [total] = useState(200);
  const [pageSize] = useState(20);
  const [data, setData] = useState(() => generateData(20));

  const columnDefs = [
    { field: 'name', headerName: '商品名称', width: 150 },
    { field: 'price', headerName: '价格', width: 100 },
    { field: 'stock', headerName: '库存', width: 100 },
    { field: 'category', headerName: '分类', width: 120 },
  ];

  return (
    <div>
      <h2>服务端分页</h2>
      <p style={{ color: '#666', marginBottom: 20 }}>total={total}，data.length={data.length}，翻页时触发 onChange 模拟请求</p>
      <Grid
        data={data}
        columnDefs={columnDefs}
        width={800}
        height={500}
        pagination={{
          total,
          pageSize,
          showSizeChanger: true,
          pageSizeOptions: [10, 20, 50],
          onChange: (page, size) => {
            const start = (page - 1) * size;
            const count = Math.min(size, total - start);
            setData(generateData(count, start));
          },
          onPageSizeChange: (_current, size) => {
            setData(generateData(Math.min(size, total), 0));
          },
        }}
        showRowNum={true}
      />
    </div>
  );
}
```
