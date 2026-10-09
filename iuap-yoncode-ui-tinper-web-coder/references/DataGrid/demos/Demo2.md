---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 操作列折叠

## 基本使用

操作按钮过多时，用 `operationColumn.maxCount` 控制直接显示的按钮数量，超出部分自动收入「更多」下拉。

```tsx
import React from 'react';
import { DataGrid } from 'tne-tinpernextpro-fe';

const data = Array.from({ length: 12 }, (_, i) => ({
  id: String(i + 1),
  name: `项目 ${i + 1}`,
  status: ['进行中', '已完成', '已挂起'][i % 3],
}));

export default function Demo2() {
  return (
    <DataGrid
      rowKey="id"
      data={data}
      columnDefs={[
        { field: 'name', headerName: '项目名称', width: 220 },
        { field: 'status', headerName: '状态', width: 120 },
      ]}
      pagination={{ current: 1, pageSize: 10 }}
      operationMode="hover"
      operations={[
        { key: 'view', text: '查看', otherProps: { colors: 'primary' }, onClick: r => console.log('查看', r) },
        { key: 'edit', text: '编辑', onClick: r => console.log('编辑', r) },
        { key: 'copy', text: '复制', onClick: r => console.log('复制', r) },
        { key: 'delete', text: '删除', onClick: r => console.log('删除', r) },
      ]}
      operationColumn={{ maxCount: 2, width: 150 }}
      height={400}
    />
  );
}
```

> `maxCount` 表格模式默认 `5`，卡片/看板视图默认 `3`。超出 `maxCount` 的操作收进「更多」菜单。`operationMode="hover"` 时操作浮在 hover 行上，可手动「显示固定操作列」。
