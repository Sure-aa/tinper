---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 合并单元格（自动合并）
启用 autoMerge 后，相邻行中值相同的单元格自动合并，通过 autoMergeColumn 控制哪些列参与自动合并

```jsx
import React, { useState } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { MergeCellsModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/mergecells';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([MergeCellsModule, RowNumbersModule]);

const data = [
  { id: '1', department: '技术部', team: '前端组', name: '张三', score: 90 },
  { id: '2', department: '技术部', team: '前端组', name: '李四', score: 85 },
  { id: '3', department: '技术部', team: '后端组', name: '王五', score: 80 },
  { id: '4', department: '技术部', team: '后端组', name: '赵六', score: 80 },
  { id: '5', department: '产品部', team: '设计组', name: '孙七', score: 75 },
  { id: '6', department: '产品部', team: '设计组', name: '周八', score: 75 },
  { id: '7', department: '产品部', team: '运营组', name: '吴九', score: 70 },
];

export default function () {
  const [mergeEnabled, setMergeEnabled] = useState(true);

  const columnDefs = [
    { field: 'department', headerName: '部门', width: 120, autoMergeColumn: true },
    { field: 'team', headerName: '团队', width: 120, autoMergeColumn: true },
    { field: 'name', headerName: '姓名', width: 120, autoMergeColumn: false },
    { field: 'score', headerName: '分数', width: 100, autoMergeColumn: true },
  ];

  return (
    <div>
      <h2>合并单元格（自动合并）</h2>
      <div style={{ marginBottom: 16 }}>
        <button onClick={() => setMergeEnabled(v => !v)}>
          {mergeEnabled ? '关闭合并' : '开启合并'}
        </button>
      </div>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={600}
        height={400}
        bordered={true}
        showRowNum={true}
        openMergeCell={mergeEnabled}
        autoMerge={mergeEnabled}
        mergeCellAlign={{ horizontal: 'center', vertical: 'middle' }}
      />
    </div>
  );
}
```
