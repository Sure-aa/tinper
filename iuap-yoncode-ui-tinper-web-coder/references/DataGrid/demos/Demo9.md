---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格 - 字段穿透 / 单号链接

## 基本使用

把列变成带权限校验的单据穿透链接：列配置 `bJointQuery` + `jointQueryOpt` 描述如何组装穿透命令，表级 `jointQuery` 控制权限与跳转。

```tsx
import React, { useState } from 'react';
import { Tag } from '@tinper/next-ui';
import { DataGrid } from 'tne-tinpernextpro-fe';

const data = [
  { id: '1', code: 'SO-2026-001', customer: '用友网络', billType: 'archive', billNo: 'SO001', serviceCode: 'sale-svc', domainKey: 'sale', detailAuth: true },
  { id: '2', code: 'SO-2026-002', customer: '星河制造', billType: 'voucher', billNo: 'SO002', serviceCode: 'sale-svc', domainKey: 'sale', detailAuth: false },
];

const columnDefs = [
  {
    field: 'code', headerName: '单据编号', width: 180, pinned: 'left',
    bJointQuery: true,
    jointQueryOpt: {
      billtype: 'billType',     // 字段名：从行数据取单据类型
      billno: 'billNo',
      rowId: 'id',
      serviceCode: 'serviceCode',
      domainKey: 'domainKey',
      othField: 'customer',     // 附加携带字段
      noPermissionMessage: '当前用户无权限查看该单据详情',
    },
  },
  { field: 'customer', headerName: '客户', width: 160 },
  { field: 'billType', headerName: '单据类型', width: 120, render: v => <Tag color={v === 'archive' ? 'info' : 'success'}>{v}</Tag> },
  { field: 'detailAuth', headerName: '详情权限', width: 120, render: (v: boolean) => <Tag color={v ? 'success' : 'danger'}>{v ? '有权限' : '无权限'}</Tag> },
];

export default function Demo9() {
  const [message, setMessage] = useState('点击单号查看穿透命令');

  return (
    <>
      <p>{message}</p>
      <DataGrid
        rowKey="id"
        data={data}
        columnDefs={columnDefs as any}
        pagination={false}
        height={300}
        width={1120}
        jointQuery={{
          hasPermission: ({ row }) => row.detailAuth,
          onNoPermission: ({ row }) => setMessage(`无权限：${row.code}`),
          open: command => { setMessage(`穿透命令：${JSON.stringify(command)}`); return false; },  // return false 阻止默认跳转
        }}
      />
    </>
  );
}
```

> 列级 `bJointQuery: true` + `jointQueryOpt`（`billtype/billno/rowId/serviceCode/domainKey/othField` 等为字段名，从行取值）组装穿透命令；表级 `jointQuery.hasPermission` 校验权限，未通过走 `onNoPermission`；`open(command)` 返回 `false` 阻止默认跳转以便完全自定义。
