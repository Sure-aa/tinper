---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础框选功能
演示单元格选择功能的多种场景，包括单击选择、拖拽框选、整行选择、整列选择、十字高亮效果。

```jsx
import React, { useState, useCallback } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { CellSelectionModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/cellselection';
import { ColumnModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/column';
import { RowSelectionModule, SelectionPresetKey } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowselection';

type ContextMenuItem = {
  label: React.ReactNode;
  type: string;
  disabled?: boolean;
  children?: any[];
  icon?: React.ReactNode;
  shortcut?: string;
};

type SelectionType = 'singleCell' | 'entireRow' | 'entireColumn' | 'range';

ModuleRegistry.registerModules([CellSelectionModule, ColumnModule, RowSelectionModule]);

interface DemoData {
  id: string;
  name: string;
  age: number;
  math: number;
  english: number;
  chinese: number;
  total: number;
  status: string;
}

const data: DemoData[] = Array.from({ length: 15 }, (_, i) => ({
    id: String(i + 1),
    name: `学生 ${i + 1}`,
    age: 16 + (i % 5),
    math: Math.floor(Math.random() * 50) + 50,
    english: Math.floor(Math.random() * 50) + 50,
    chinese: Math.floor(Math.random() * 50) + 50,
    total: 0,
    status: i % 6 === 0 ? 'leave' : i % 5 === 0 ? 'absent' : 'present',
  })).map(item => ({
    ...item,
    total: item.math + item.english + item.chinese,
  }));
export default function CellSelectionDemo() {
  const [selectionInfo, setSelectionInfo] = useState<string>('未选择任何单元格');
  const [activeCell, setActiveCell] = useState<any>(null);
  const [gridApi, setGridApi] = useState<any>(null);

  // 自定义菜单项
  const customMenuItems: ContextMenuItem[] = [
    { label: '格式化单元格', type: 'formatCells', shortcut: 'Ctrl+Shift+F' },
    { label: '-', type: 'separator' },
    { label: '设置状态', type: 'setStatus', icon: '⚙' },
  ];



  const columnDefs = [
    {
      field: 'id',
      headerName: '学号',
      width: 80,
      pinned: 'left',
    },
    {
      field: 'name',
      headerName: '姓名',
      width: 100,
    },
    {
      field: 'age',
      headerName: '年龄',
      width: 80,
    },
    {
      field: 'math',
      headerName: '数学',
      width: 90,
      editable: true,
    },
    {
      field: 'english',
      headerName: '英语',
      width: 90,
      editable: true,
    },
    {
      field: 'chinese',
      headerName: '语文',
      width: 90,
      editable: true,
    },
    {
      field: 'total',
      headerName: '总分',
      width: 90,
      valueGetter: (params: any) => {
        return params.data.math + params.data.english + params.data.chinese;
      },
    },
    {
      field: 'status',
      headerName: '状态',
      width: 100,
      render: (value: string) => {
        const colors = {
          present: '#52c41a',
          absent: '#faad14',
          leave: '#ff4d4f',
        };
        const labels = {
          present: '出勤',
          absent: '缺勤',
          leave: '请假',
        };
        return (
          <span style={{ color: colors[value as keyof typeof colors] || '#999' }}>
            {labels[value as keyof typeof labels] || value}
          </span>
        );
      },
    },
  ];

  const handleSelectionChange = useCallback((event: any, rowKeys: string[], columnKeys: string[]) => {
    let info = '';

    if (rowKeys && rowKeys.length > 0 && columnKeys && columnKeys.length > 0) {
      if (rowKeys.length === 1 && columnKeys.length === 1) {
        info = `单元格: [行：${rowKeys[0]}, 列：${columnKeys[0]}]`;
      } else {
        info = `已选择 ${rowKeys.length} 行, ${columnKeys.length} 列`;
      }
    } else {
      info = '未选择任何单元格';
    }
    setSelectionInfo(info);
  }, []);

  const handleClearSelection = () => {
    if (gridApi) {
      gridApi.clearSelection();
      setSelectionInfo('已清空选择');
    }
  };

  const handleSelectFirstRow = (event: React.MouseEvent) => {
    // 因为表格以外的点击事件都会清空框选，所以使用了setTimeout，避免表格点击事件触发清空选择
    if (gridApi) {
      setTimeout(() => {
        gridApi?.selectEntireRow(0, event);
      }, 0);
    }
  };

  const handleSelectMathColumn = (event: React.MouseEvent) => {
    // 因为表格以外的点击事件都会清空框选，所以使用了setTimeout，避免表格点击事件触发清空选择
    if (gridApi) {
      setTimeout(() => {
        gridApi?.selectEntireColumn("math", event);
      }, 0);
    }
  };

  const handleCustomMenuClick = (type: string, rowKeys: string[], colKeys: string[], selectionType: SelectionType) => {
    console.log('Custom menu item clicked:', { type, rowKeys, colKeys, selectionType });

    switch (type) {
      case 'custom1':
        alert(`选中单元格：${rowKeys.join(', ')} ${colKeys.join(', ')}`);
        break;
      case 'custom2':
        alert(`选中单元格：${rowKeys.join(', ')} ${colKeys.join(', ')}`);
        break;
    }
  };

  const handleSelectRange = () => {
    // 因为表格以外的点击事件都会清空框选，所以使用了setTimeout，避免表格点击事件触发清空选择
    if (gridApi) {
      const range = {
        "start": {
          "rowKey": "2",
          "columnKey": "age"
        },
        "end": {
          "rowKey": "4",
          "columnKey": "math"
        },
        "rowKeys": [
          "2",
          "3",
          "4"
        ],
        "columnKeys": [
          "age",
          "math"
        ]
      }
      setTimeout(() => {
        gridApi?.setSelectionRange(range);
      }, 0);
    }
  };

  return (
    <div style={{ padding: 20 }}>
      <div style={{ marginBottom: 16 }}>
        <h3 style={{ marginBottom: 8 }}>单元格选择功能演示</h3>
        <p style={{ color: '#666', marginBottom: 12 }}>
          拖拽选择多个单元格，按住 Ctrl/Cmd 点击单独选择，按住 Shift 选择连续范围
        </p>
        <div style={{ display: 'flex', gap: 8, flexWrap: 'wrap', marginBottom: 12 }}>
          <button onClick={handleClearSelection} style={btnStyle}>
            清空选择
          </button>
          <button onClick={handleSelectFirstRow} style={btnStyle}>
            选中第一行
          </button>
          <button onClick={handleSelectMathColumn} style={btnStyle}>
            选中数学列
          </button>
          <button onClick={handleSelectRange} style={btnStyle}>
            选中框选范围
          </button>
        </div>
        <div style={{
          padding: '12px 16px',
          background: '#f5f5f5',
          borderRadius: 4,
          fontFamily: 'monospace',
          fontSize: 13,
        }}>
          <strong>当前选择:</strong> {selectionInfo}
          {activeCell && (
            <span style={{ marginLeft: 16 }}>
              <strong>活动单元格:</strong> [{activeCell.rowKey}, {activeCell.columnKey}]
            </span>
          )}
        </div>
      </div>

      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        fieldid="cellSelectionDemo"
        width={900}
        hideDefaultMenu={false}
        height={450}
        popMenu={(rowKeys: string[], colKeys: string[]) => [
          { label: '自定义1', type: 'custom1' },
          { label: '自定义2', type: 'custom2' }]}
        onPopMenuClick={handleCustomMenuClick}
        showRowNum={true}
        cellSelection= {true}
        onSelectionChange={handleSelectionChange}
        onReady={(params: any) => {
          setGridApi(params);
        }}
        rowNumbers={{
          enabled: true,
        }}
        rowSelection={{
          mode: 'multiRow'
        }}
      />
    </div>
  );
}

const btnStyle: React.CSSProperties = {
  padding: '6px 12px',
  fontSize: 13,
  border: '1px solid #d9d9d9',
  borderRadius: 4,
  background: '#fff',
  cursor: 'pointer',
  transition: 'all 0.2s',
};
```
