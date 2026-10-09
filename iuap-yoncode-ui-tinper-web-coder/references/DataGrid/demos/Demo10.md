---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 卡片与看板模式

## 基本使用

同一份 `columnDefs` 数据，通过 `displayMode` 在表格 / 卡片 / 看板三种视图间切换，复用分页、选择、操作列、空态能力。

```tsx
import React, { useState } from 'react';
import { DataGrid } from 'tne-tinpernextpro-fe';

type DisplayMode = 'table' | 'card' | 'kanban';

const data = [
  { id: '1', code: '笔记本', customer: '信息部门', encoded: 'IT-001', status: '在用', stage: 'todo' },
  { id: '2', code: '投影仪', customer: '会议室', encoded: 'IT-002', status: '闲置', stage: 'doing' },
  { id: '3', code: '打印机', customer: '行政部', encoded: 'IT-003', status: '已报废', stage: 'done' },
];

const stageGroups = [
  { text: '在用', value: 'todo' },
  { text: '闲置', value: 'doing' },
  { text: '已报废', value: 'done' },
];

export default function Demo10() {
  const [displayMode, setDisplayMode] = useState<DisplayMode>('table');
  const [selectedRowKeys, setSelectedRowKeys] = useState<React.Key[]>([]);

  return (
    <DataGrid
      rowKey="id"
      data={data}
      columnDefs={[
        { field: 'code', headerName: '标题', width: 200 },
        { field: 'customer', headerName: '信息1', width: 200, cardLabelVisible: false },
        { field: 'encoded', headerName: '信息2', width: 200, cardLabelVisible: false },
        { field: 'status', headerName: '状态', width: 110 },
      ]}
      displayMode={displayMode}
      displayModeSwitchVisible
      pagination={{ current: 1, pageSize: 6, showTotal: t => `共 ${t} 条` }}
      rowSelection={{ mode: 'multiRow', selectedRowKeys, onChange: e => setSelectedRowKeys(e.selectedKeys) }}
      cardConfig={{
        titleField: 'code',
        statusField: 'status',
        statusStyle: ({ value }) => (value === '闲置' ? { backgroundColor: 'orange' } : undefined),
        showStatus: true,
        showSelectAll: true,
        onModeChange: mode => setDisplayMode(mode),
      }}
      kanbanConfig={{
        groupField: 'stage',
        groupList: stageGroups,
        onModeChange: mode => setDisplayMode(mode),
      }}
      operations={[
        { key: 'repair', text: '报废申请', onClick: r => console.log('报废', r.code) },
        { key: 'transfer', text: '转移申请', onClick: r => console.log('转移', r.code) },
      ]}
      operationColumn={{ width: 200, maxCount: 3 }}
      emptyConfig={{ emptyText: '暂无资产卡片数据' }}
      height={420}
      width={1120}
    />
  );
}
```

> `displayMode`（受控）+ `displayModeSwitchVisible` 显示切换 Radio。`cardConfig` 配置卡片（`titleField/statusField/statusStyle/imageField/showSelectAll` 等，列上 `cardLabelVisible:false` 隐藏字段标签）；`kanbanConfig.groupField` 按字段分列、`groupList` 预定义分组顺序与占位空组。卡片/看板操作 `maxCount` 默认 `3`。
