---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 业务行号 LineNo

## 基本使用

业务行号是**数据字段**（支持小数），区别于 `showRowNum` 渲染的页面自然序号。列声明 `cControlType: 'lineno'`，配置 `lineNo` 控制生成方式（二分插入 / 自动步长）。

```tsx
import React, { useRef, useState } from 'react';
import { Button, Space, Tag } from '@tinper/next-ui';
import { DataGrid } from 'tne-tinpernextpro-fe';

const statusColor: Record<string, string> = { draft: 'default', confirmed: 'success' };

const createRow = (lineNo: number) => ({
  id: String(Date.now() + Math.random()),
  lineNo,
  material: `MAT-${lineNo}`,
  name: '物料',
  quantity: 1,
  status: 'draft',
});

const initialData = Array.from({ length: 3 }, (_, i) => createRow((i + 1) * 10));

export default function Demo8() {
  const tableRef = useRef<any>(null);
  const [data, setData] = useState(initialData);
  const [generateType, setGenerateType] = useState<'binary' | 'auto'>('binary');

  return (
    <>
      <Space style={{ marginBottom: 12 }}>
        <Button onClick={() => setGenerateType(g => (g === 'binary' ? 'auto' : 'binary'))}>
          生成方式：{generateType}（点击切换）
        </Button>
        <Button onClick={() => setData(tableRef.current?.insertRow(1, createRow(0)) || data)}>在第 2 行处插入</Button>
        <Button onClick={() => setData(tableRef.current?.appendRow(createRow(0)) || data)}>追加行</Button>
        <Button onClick={() => setData(tableRef.current?.regenerateLineNo() || data)}>重排行号</Button>
      </Space>
      <DataGrid
        ref={tableRef}
        rowKey="id"
        data={data}
        columnDefs={[
          { field: 'lineNo', headerName: '业务行号', cControlType: 'lineno', width: 110, pinned: 'left', align: 'right' },
          { field: 'material', headerName: '物料编码', width: 140, pinned: 'left' },
          { field: 'name', headerName: '名称', width: 160 },
          { field: 'quantity', headerName: '数量', width: 100, align: 'right', fieldType: 'number' },
          { field: 'status', headerName: '状态', width: 120, render: v => <Tag color={statusColor[v]}>{v}</Tag> },
        ]}
        pagination={false}
        showRowNum={{ width: 58, pinned: 'left' }}
        lineNo={{
          generateType,    // 'binary'(二分插入，前后取中值) | 'auto'(按步长连续编号)
          step: 10,
          onDataChange: next => setData(next),
        }}
        height={360}
        width={980}
      />
    </>
  );
}
```

> `cControlType: 'lineno'` 声明业务行号列；`generateType: 'binary'` 在前后行号取中值（便于中间插行），`'auto'` 按 `step` 连续编号。`insertRow/appendRow/regenerateLineNo` 通过 ref 调用；`setDataSource/appendRow/insertRow` 可带 `options.generateLineNo`。
