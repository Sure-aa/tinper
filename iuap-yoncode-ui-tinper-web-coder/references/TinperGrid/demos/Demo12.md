---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础行拖拽排序
启用 rowDrag 后第一列出现拖拽手柄，拖拽可重新排列行的顺序

```jsx
import React, { useState } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowDragModule, reorderDataByDrag } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowdrag';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([RowDragModule, RowNumbersModule]);

export default function() {
  const [data, setData] = useState([
    { id: 1, name: '张三', age: 28, city: '北京', department: '技术部' },
    { id: 2, name: '李四', age: 32, city: '上海', department: '市场部' },
    { id: 3, name: '王五', age: 25, city: '深圳', department: '产品部' },
    { id: 4, name: '赵六', age: 30, city: '杭州', department: '技术部' },
    { id: 5, name: '钱七', age: 27, city: '成都', department: '设计部' },
    { id: 6, name: '孙八', age: 35, city: '广州', department: '市场部' },
    { id: 7, name: '周九', age: 29, city: '武汉', department: '产品部' },
    { id: 8, name: '吴十', age: 31, city: '西安', department: '技术部' },
  ]);

  const columnDefs = [
    { field: 'name', headerName: '姓名', width: 120 },
    { field: 'age', headerName: '年龄', width: 100 },
    { field: 'city', headerName: '城市', width: 120 },
    { field: 'department', headerName: '部门', width: 150 },
  ];

  return (
    <div>
      <h2>行拖拽排序</h2>
      <Grid
        data={data}
        columnDefs={columnDefs}
        width={800}
        height={400}
        rowHeight={40}
        rowKey="id"
        showRowNum={true}
        rowDrag={{
          enabled: true,
          onRowReorderEnd: (event) => setData(reorderDataByDrag(data, event)),
          onRowReorderStart: (rowIndex) => console.log('开始拖拽行:', rowIndex),
        }}
      />
    </div>
  );
}
```
