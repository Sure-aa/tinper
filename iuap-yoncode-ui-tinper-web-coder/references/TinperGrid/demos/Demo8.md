---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 行多选
多选模式（checkbox）支持受控模式管理选中状态，支持自定义下拉菜单项

```jsx
import React, { useState } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowSelectionModule, SelectionPresetKey } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';
import { PaginationModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/pagination';
import { Tag } from '@tinper/next-ui';

ModuleRegistry.registerModules([RowSelectionModule, PaginationModule]);

export default function () {
  const [selectedRowKeys, setSelectedRowKeys] = useState(['1', '2', '3']);

  const data = Array.from({ length: 50 }, (_, i) => ({
    id: String(i + 1),
    name: `用户 ${i + 1}`,
    age: 18 + (i % 60),
    email: `user${i + 1}@example.com`,
    department: ['研发部', '产品部', '设计部', '市场部'][i % 4],
    status: 'active',
  }));

  const columnDefs = [
    { field: 'name', headerName: '姓名', width: 120 },
    { field: 'age', headerName: '年龄', width: 80 },
    { field: 'email', headerName: '邮箱', width: 200 },
    { field: 'department', headerName: '部门', width: 120 },
    {
      field: 'status', headerName: '状态', width: 100,
      render: (value) => (
        <Tag color={value === 'disabled' ? 'invalid' : 'success'}>
          {value === 'disabled' ? '已禁用' : '正常'}
        </Tag>
      ),
    },
  ];

  return (
    <div>
      <div style={{ marginBottom: 16 }}>已选中 {selectedRowKeys.length} 行</div>
      <Grid
        data={data}
        columnDefs={columnDefs}
        bordered
        rowKey="id"
        width={800}
        height={500}
        fillSpace
        pagination={{ defaultCurrent: 1, defaultPageSize: 20 }}
        rowSelection={{
          mode: 'multiRow',
          showSelectedFilter: true,
          selectedRowKeys,
          selections: [
            SelectionPresetKey.SELECTION_ALL,
            SelectionPresetKey.SELECTION_CURRENT_PAGE,
            SelectionPresetKey.SELECTION_INVERT,
            SelectionPresetKey.SELECTION_NONE,
            {
              key: 'selectDev',
              text: '选择研发部',
              onSelect: (changableRowKeys) => {
                const devKeys = data
                  .filter(row => row.department === '研发部')
                  .map(row => row.id)
                  .filter(key => changableRowKeys.includes(key));
                setSelectedRowKeys(devKeys);
              }
            },
          ],
          onChange: (event) => setSelectedRowKeys(event.selectedKeys),
        }}
      />
    </div>
  );
}
```

## 行单选
单选模式（singleRow），点击行即可选中，常用于需要选择单条记录的场景

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowSelectionModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';

ModuleRegistry.registerModules([RowSelectionModule]);

export default function () {
  const data = Array.from({ length: 20 }, (_, i) => ({
    id: String(i + 1),
    product: `商品 ${i + 1}`,
    price: (100 + i * 50).toFixed(2),
    stock: 100 + (i % 500),
    category: ['电子产品', '图书', '服装', '食品', '家居'][i % 5],
    rating: (4 + Math.random()).toFixed(1),
  }));

  const columnDefs = [
    { field: 'product', headerName: '商品名称', width: 150 },
    { field: 'price', headerName: '价格', width: 100, render: (value) => `¥${value}` },
    { field: 'stock', headerName: '库存', width: 100 },
    { field: 'category', headerName: '分类', width: 120 },
    { field: 'rating', headerName: '评分', width: 100, render: (value) => `⭐ ${value}` },
  ];

  return (
    <div>
      <h2>行单选</h2>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={400}
        rowSelection={{
          mode: 'singleRow',
          onChange: (event) => {
            console.log('选择变化:', event.selectedKeys[0], event.selectedRows[0]);
          },
        }}
      />
    </div>
  );
}
```
