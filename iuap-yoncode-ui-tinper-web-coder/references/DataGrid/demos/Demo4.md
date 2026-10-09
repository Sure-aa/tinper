---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 树表懒加载

## 基本使用

配置 `loadData`（返回 Promise）后，组件**自动识别为树表**，展开非叶子节点时异步加载子节点，无需显式传 `treeData`。可用 `childrenColumnName` 自定义子节点字段。

```tsx
import React from 'react';
import { Tag } from '@tinper/next-ui';
import { DataGrid } from 'tne-tinpernextpro-fe';

// 节点用 isLeaf 标识是否叶子；非叶子节点展开时触发 loadData
const rootData = [
  { id: '1', name: '总部', type: '组织', manager: '张三', status: 'active', isLeaf: false, subRows: [] },
  { id: '2', name: '华东大区', type: '大区', manager: '李四', status: 'active', isLeaf: false, subRows: [] },
];

const lazyChildrenMap: Record<string, any[]> = {
  '1': [
    { id: '1-1', name: '财务部', type: '部门', manager: '王五', status: 'active', isLeaf: true },
    { id: '1-2', name: '人事部', type: '部门', manager: '赵六', status: 'active', isLeaf: true },
  ],
  '2': [
    { id: '2-1', name: '上海分公司', type: '部门', manager: '钱七', status: 'active', isLeaf: true },
  ],
};

const statusColor: Record<string, string> = { active: 'success', inactive: 'default' };

export default function Demo4() {
  const loadData = (record: any) => new Promise<any[]>(resolve => {
    setTimeout(() => resolve(lazyChildrenMap[record.id] || []), 600);
  });

  return (
    <DataGrid
      rowKey="id"
      childrenColumnName="subRows"
      data={rootData}
      columnDefs={[
        { field: 'name', headerName: '组织/项目', width: 220, pinned: 'left' },
        { field: 'type', headerName: '类型', width: 120 },
        { field: 'manager', headerName: '负责人', width: 120 },
        { field: 'status', headerName: '状态', width: 120, render: v => <Tag color={statusColor[v]}>{v}</Tag> },
      ]}
      pagination={false}
      loadData={loadData}
      rowSelection={{ mode: 'multiRow' }}
      height={360}
      width={760}
    />
  );
}
```

> 节点用 `isLeaf: true` 标识叶子（不展开）。`loadData` 返回 Promise，配置后自动开启树表模式，**无需再传 `treeData`**。
