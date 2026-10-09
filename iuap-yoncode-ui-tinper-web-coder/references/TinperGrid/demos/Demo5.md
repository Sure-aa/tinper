---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 列设置
展示列对齐、隐藏、表头显示、边框、斑马纹、加载态等基础列配置

```jsx
import React, { useState, useMemo } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { ColumnModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/column';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';
import { Radio, Space, Switch, Divider } from '@tinper/next-ui';

ModuleRegistry.registerModules([ColumnModule, RowNumbersModule]);

export default function () {
  const [align, setAlign] = useState('left');
  const [hide, setHide] = useState(false);
  const [showHeader, setShowHeader] = useState(true);
  const [bordered, setBordered] = useState(false);
  const [stripeLine, setStripeLine] = useState(false);
  const [loading, setLoading] = useState(false);
  const [enableFillRemainingWidth, setEnableFillRemainingWidth] = useState(true);

  const data = Array.from({ length: 20 }, (_, i) => ({
    id: i + 1,
    name: `用户 ${i + 1}`,
    age: 18 + (i % 60),
    email: `user${i + 1}@example.com`,
    department: ['研发部', '产品部', '设计部', '市场部'][i % 4],
  }));

  const columnDefs = useMemo(() => [
    { field: 'name', headerName: <span>姓名</span>, width: '20%', align, tip: '姓名', cellStyle: { color: 'blue', cursor: 'pointer' }, onCellClick: (params) => console.log(params) },
    { field: 'age', headerName: () => '年龄', align, hide },
    { field: 'email', headerName: '邮箱', width: '180px', align, headerStyle: { color: 'red' } },
    { field: 'department', headerName: '部门', width: '120', align },
  ], [align, hide]);

  return (
    <div>
      <h2>列设置</h2>
      <div style={{ padding: 16, border: '1px solid #e5e5e5', borderRadius: 4, marginBottom: 16, display: 'flex', flexDirection: 'column' }}>
        <Space>
          <span>align:</span>
          <Radio.Group value={align} onChange={(v) => setAlign(v)}>
            <Radio value="left">left</Radio>
            <Radio value="center">center</Radio>
            <Radio value="right">right</Radio>
          </Radio.Group>
          <span>年龄 hide:</span>
          <Switch checked={hide} onChange={(v) => setHide(v)} />
          <span>enableFillRemainingWidth:</span>
          <Switch checked={enableFillRemainingWidth} onChange={(v) => setEnableFillRemainingWidth(v)} />
        </Space>
        <Divider style={{ margin: '16px 0' }} />
        <Space>
          <span>bordered:</span>
          <Switch checked={bordered} onChange={(v) => setBordered(v)} />
          <span>stripeLine:</span>
          <Switch checked={stripeLine} onChange={(v) => setStripeLine(v)} />
          <span>loading:</span>
          <Switch checked={loading} onChange={(v) => setLoading(v)} />
          <span>showHeader:</span>
          <Switch checked={showHeader} onChange={(v) => setShowHeader(v)} />
        </Space>
      </div>
      <Grid
        data={data}
        columnDefs={columnDefs}
        height={500}
        showHeader={showHeader}
        showRowNum={true}
        bordered={bordered}
        stripeLine={stripeLine}
        loading={loading}
        enableFillRemainingWidth={enableFillRemainingWidth}
        fillSpace={true}
      />
    </div>
  );
}
```
