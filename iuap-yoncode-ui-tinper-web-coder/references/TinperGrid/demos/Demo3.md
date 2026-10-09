---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 大数据
大数据量渲染

```jsx
import React, { useMemo } from 'react';
import { Grid, ColumnDef, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([RowNumbersModule]);

export default function BigDataDemo() {
  // 生成 250 列定义
  const columnDefs = useMemo(() => {
    const cols: ColumnDef[] = [
      { field: 'name', headerName: '姓名', width: 100, fixed: true },
    ];

    // 添加 248 列动态数据列
    for (let i = 1; i <= 248; i++) {
      cols.push({
        field: `col${i}`,
        headerName: `列${i}`,
        width: 100,
        allowCellsRecycling: true,
      });
    }

    return cols;
  }, []);

  // 生成 10000 行数据
  const data = useMemo(() => {
    return Array.from({ length: 10000 }, (_, rowIndex) => {
      const row: Record<string, any> = {
        id: rowIndex + 1,
        name: `用户${rowIndex + 1}`,
      };

      // 添加 248 列数据
      for (let i = 1; i <= 248; i++) {
        row[`col${i}`] = `R${rowIndex + 1}C${i}`;
      }

      return row;
    });
  }, []);

  return (
    <div>
      <h2>大数据量渲染示例</h2>
      <p style={{ color: '#666', marginBottom: 20 }}>
        数据规模: {data.length.toLocaleString()} 行 × {columnDefs.length} 列 = {(data.length * columnDefs.length).toLocaleString()} 个单元格
      </p>
      <p style={{ color: '#999', marginBottom: 20, fontSize: 12 }}>
        基于虚拟滚动技术，只渲染可视区域内的行和列，保证大数据量下的流畅体验
      </p>
      <Grid
        data={data}
        columnDefs={columnDefs}
        showRowNum={true}
        rowHeight={35}
        height={680}
        allowCellsRecycling={true}
        fillSpace
      />
    </div>
  );
}
```
