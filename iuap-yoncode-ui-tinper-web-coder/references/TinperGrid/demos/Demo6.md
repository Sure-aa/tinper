---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 多级表头
通过 columnDefs 的 children 配置多级表头结构，支持嵌套分组和列固定

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { ColumnModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/column';
import { ColumnPinnedModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/columnpinned';

ModuleRegistry.registerModules([ColumnModule, ColumnPinnedModule]);

export default function() {
  const data = Array.from({ length: 20 }, (_, i) => ({
    id: i,
    name: "John Brown" + i,
    age: 18 + (i % 60),
    street: "Lake Park",
    building: "C",
    basic: "五",
    number: 2035,
    companyAddress: "北清路 68 号",
    companyName: "用友",
    gender: i % 2 === 0 ? "男" : "女"
  }));

  const columnDefs = [
    { field: "name", headerName: "姓名", width: 120, fixed: "left" },
    {
      headerName: "个人信息",
      groupId: "personalInfo",
      width: 500,
      children: [
        { field: "age", headerName: "年龄", width: 80 },
        {
          headerName: "地址",
          width: 400,
          groupId: "address",
          children: [
            { field: "street", headerName: "街道", width: 100 },
            {
              headerName: "单元",
              width: 300,
              groupId: "unit",
              children: [
                { field: "building", headerName: "楼号", width: 100 },
                { field: "basic", headerName: "单元", width: 100 },
                { field: "number", headerName: "门户", width: 100 }
              ]
            }
          ]
        }
      ]
    },
    {
      headerName: "公司信息",
      groupId: "businessInfo",
      width: 400,
      children: [
        { field: "companyAddress", headerName: "公司地址", width: 200 },
        { field: "companyName", headerName: "公司名称", width: 200 }
      ]
    },
    { field: "gender", headerName: "性别", width: 100 }
  ];

  return (
    <div>
      <h2>多级表头</h2>
      <Grid
        data={data}
        columnDefs={columnDefs}
        height={500}
        groupHeaderHeight={30}
        fillSpace={true}
        enableFillRemainingWidth
        enablePinned={true}
        suppressResizeColumns={true}
        suppressMovableColumns={true}
      />
    </div>
  );
}
```
