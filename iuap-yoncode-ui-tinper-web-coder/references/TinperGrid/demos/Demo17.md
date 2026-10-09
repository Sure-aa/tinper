---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 行悬浮操作按钮
鼠标悬浮到行时显示操作按钮，支持切换为固定列模式（图标或文字链接）

```jsx
import React, { useState } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowStyleModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowstyle';
import { RowHoverModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowhover';
import { ColumnPinnedModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/columnpinned';
import { Button, Message, Tag } from '@tinper/next-ui';

ModuleRegistry.registerModules([RowStyleModule, RowHoverModule, ColumnPinnedModule]);

export default function () {
  const [data, setData] = useState(() =>
    Array.from({ length: 20 }, (_, i) => ({
      id: String(i + 1),
      name: `员工 ${i + 1}`,
      age: 25 + (i % 20),
      department: ['技术部', '产品部', '设计部', '运营部'][i % 4],
      status: ['在职', '离职', '试用期'][i % 3],
      email: `employee${i + 1}@company.com`,
    }))
  );

  const [displayMode, setDisplayMode] = useState('hover');

  const columnDefs = [
    { field: 'name', headerName: '姓名', width: 120 },
    { field: 'age', headerName: '年龄', width: 80 },
    { field: 'department', headerName: '部门', width: 120 },
    {
      field: 'status', headerName: '状态', width: 100,
      render: (value) => {
        const colorMap = { 在职: 'success', 离职: 'invalid', 试用期: 'info' };
        return <Tag color={colorMap[value]}>{value}</Tag>;
      },
    },
    { field: 'email', headerName: '邮箱', width: 220 },
  ];

  const handleEdit = (rowData) => {
    Message.create({ content: `编辑：${rowData.name}`, color: 'info' });
  };

  const handleDelete = (rowKey, rowData) => {
    Message.create({ content: `删除：${rowData.name}`, color: 'warning' });
    setData((prev) => prev.filter((item) => item.id !== rowKey));
  };

  return (
    <div>
      <div style={{ marginBottom: 16 }}>
        <Button size="sm" type={displayMode === 'hover' ? 'primary' : 'default'} onClick={() => setDisplayMode('hover')}>Hover 模式</Button>
        <p style={{ color: '#666', marginTop: 8 }}>当前模式：鼠标悬浮到任意行，右侧会显示操作按钮</p>
      </div>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={500}
        rowHover={{
          position: 'right',
          offset: 10,
          rowHoverContent: ({ rowKey, rowData }) => (
            <div style={{ display: 'flex', gap: 8, height: '100%', justifyContent: 'center', alignItems: 'center', padding: '4px 8px' }}>
              <Button size="small" colors="dark" onClick={(e) => { e.stopPropagation(); handleEdit(rowData); }}>编辑</Button>
              <Button size="small" colors="dark" onClick={(e) => { e.stopPropagation(); handleDelete(rowKey, rowData); }}>删除</Button>
            </div>
          ),
        }}
      />
    </div>
  );
}
```
