---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 空状态配置

## 基本使用

`emptyConfig` 区分两种空态：**数据源为空**（`empty`）与**有数据但筛选无结果**（`searchEmpty`），分别配置文案和下方自定义内容。

```tsx
import React, { useRef, useState } from 'react';
import { Button, Space } from '@tinper/next-ui';
import { DataGrid } from 'tne-tinpernextpro-fe';

export default function Demo3() {
  const tableRef = useRef<any>(null);
  const [data, setData] = useState([
    { id: '1', code: 'OBJ-001', name: '采购申请', status: '草稿' },
    { id: '2', code: 'OBJ-002', name: '销售订单', status: '已确认' },
  ]);

  // 程序化触发「筛选无结果」
  const applyNoResultFilter = () => {
    tableRef.current?.api?.setTextFilter?.('name', 'equals', '__NO_RESULT__');
    tableRef.current?.api?.applyFilters?.('name', 'text');
  };
  const clearFilter = () => tableRef.current?.api?.clearFilter?.('name', true);
  const addRow = () => setData(d => [...d, { id: String(Date.now()), code: 'NEW', name: '新增对象', status: '草稿' }]);

  return (
    <DataGrid
      ref={tableRef}
      rowKey="id"
      data={data}
      columnDefs={[
        { field: 'code', headerName: '对象编码', width: 140, filter: 'textFilter' },
        { field: 'name', headerName: '业务对象', width: 180, filter: 'textFilter' },
        { field: 'status', headerName: '状态', width: 120, filter: 'setFilter' },
      ]}
      pagination={false}
      emptyConfig={{
        emptyText: '暂无数据，建议您手动新增业务对象',
        searchEmptyText: '暂无数据，建议您更换查询方案',
        extra: <Button colors="primary" onClick={addRow}>新增业务对象</Button>,
        searchExtra: (
          <Space>
            <Button onClick={clearFilter}>重置查询</Button>
            <Button colors="primary" onClick={addRow}>新增业务对象</Button>
          </Space>
        ),
      }}
      height={360}
      width={760}
    />
  );
}
```

> `emptyText` / `extra` 对应数据源为空；`searchEmptyText` / `searchExtra` 对应筛选无结果（未传时回退到 `emptyText` / `extra`）。可通过 `ref.api.setTextFilter / applyFilters / clearFilter` 程序化触发筛选以演示两种空态。
