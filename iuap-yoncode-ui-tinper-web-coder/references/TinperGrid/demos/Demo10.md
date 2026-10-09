---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础树表
树形数据展示，支持展开/折叠、过滤、点击行展开等功能

```jsx
import React, { useState, useRef } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { TreeModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/tree';
import { FilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/filter';
import { TextFilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/textfilter';
import { NumberFilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/numberfilter';
import { SetFilterModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/setfilter';
import { Button, Switch } from '@tinper/next-ui';

ModuleRegistry.registerModules([TreeModule, FilterModule, TextFilterModule, NumberFilterModule, SetFilterModule]);

export default function TreeBasicDemo() {
  const gridRef = useRef(null);
  const [expandRowByClick, setExpandRowByClick] = useState(true);

  const [data] = useState([
    {
      id: '1', name: '研发中心', type: '部门', headcount: 120, budget: 5000000,
      children: [
        {
          id: '1-1', name: '前端组', type: '小组', headcount: 30, budget: 1200000,
          children: [
            { id: '1-1-1', name: 'React 团队', type: '团队', headcount: 12, budget: 500000 },
            { id: '1-1-2', name: 'Vue 团队', type: '团队', headcount: 10, budget: 400000 },
          ],
        },
        {
          id: '1-2', name: '后端组', type: '小组', headcount: 45, budget: 1800000,
          children: [
            { id: '1-2-1', name: 'Java 团队', type: '团队', headcount: 20, budget: 800000 },
            { id: '1-2-2', name: 'Go 团队', type: '团队', headcount: 15, budget: 600000 },
          ],
        },
        { id: '1-3', name: '测试组', type: '小组', headcount: 25, budget: 800000 },
      ],
    },
    {
      id: '2', name: '产品中心', type: '部门', headcount: 60, budget: 2500000,
      children: [
        { id: '2-1', name: '产品设计组', type: '小组', headcount: 20, budget: 800000 },
        { id: '2-2', name: 'UI/UX 组', type: '小组', headcount: 25, budget: 1000000 },
      ],
    },
    { id: '3', name: '市场中心', type: '部门', headcount: 40, budget: 3000000 },
  ]);

  const columnDefs = [
    { field: 'name', headerName: '名称', width: 250, filter: 'setFilter' },
    { field: 'type', headerName: '类型', width: 100, filter: 'textFilter' },
    { field: 'headcount', headerName: '人数', width: 100, align: 'right', filter: 'numberFilter' },
    { field: 'budget', headerName: '预算', width: 150, align: 'right', render: (value) => `¥${value.toLocaleString()}`, filter: 'numberFilter' },
  ];

  return (
    <div>
      <h3>基础树表</h3>
      <div style={{ marginBottom: 12, display: 'flex', gap: 8, alignItems: 'center' }}>
        <Button onClick={() => gridRef.current?.api?.expandAll()}>展开全部</Button>
        <Button onClick={() => gridRef.current?.api?.collapseAll()}>折叠全部</Button>
        <Button onClick={() => gridRef.current?.api?.clearFilter()}>清除过滤</Button>
        <Switch checked={expandRowByClick} onChange={(checked) => setExpandRowByClick(checked)} />
        <span>点击行展开</span>
      </div>
      <Grid
        ref={gridRef}
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={800}
        height={500}
        enableFilter={true}
        treeData={true}
        childrenColumnName="children"
        indentSize={20}
        expandIconColumnIndex={0}
        defaultExpandedRowKeys={['1']}
        expandRowByClick={expandRowByClick}
        onExpand={(expanded, record) => console.log('展开变化:', record.name, expanded ? '展开' : '折叠')}
      />
    </div>
  );
}
```
