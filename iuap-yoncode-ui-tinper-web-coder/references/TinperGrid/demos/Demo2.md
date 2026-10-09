---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 文字换行行数限制
超出指定行数显示省略号(本示例lineClamp为3, 最多显示3行)

```jsx
import React from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([RowNumbersModule]);

/**
 * 文字换行行数限制
 * 超出指定行数显示省略号(本示例lineClamp为3, 最多显示3行)
 */
export default function AutoRowHeightExample() {
  // 模拟数据 - 包含不同长度的文本
  const data = [
    {
      id: 1,
      name: '张三',
      description: '这是一段简短的描述',
      content: '正常内容'
    },
    {
      id: 2,
      name: '李四',
      description: '这是一段很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长的描述文本，需要换行显示',
      content: '这也是一段很长的内容，包含了很多信息，需要多行来展示。这样可以更好地展示自适应行高的效果。'
    },
    {
      id: 3,
      name: '王五',
      description: '中等长度的描述文本，大概需要两到三行来显示',
      content: '普通内容'
    },
    {
      id: 4,
      name: '赵六',
      description: '短描述',
      content: '超级长的内容文本，包含大量信息。在实际业务场景中，这种情况很常见，比如用户评论、商品描述、文章摘要等等等等等等等等等等等等等等等。自适应行高可以确保所有内容都能完整显示，而不会被截断。'
    },
    {
      id: 5,
      name: '孙七',
      description: '正常的描述文本',
      content: '短内容'
    },
  ];

  // 列定义
  const columnDefs = [
    {
      field: 'name',
      headerName: '姓名',
      width: 100,
    },
    {
      field: 'description',
      headerName: '描述',
      width: 250,
    },
    {
      field: 'content',
      headerName: '内容',
      width: 300,
    },
  ];

  return (
    <div style={{ padding: '20px' }}>
      <h2>文字换行行数限制</h2>
      <p>超出指定行数显示省略号(本示例lineClamp为3, 最多显示3行)</p>

      <div style={{ marginTop: '20px' }}>
        <Grid
          data={data}
          columnDefs={columnDefs}
          width={800}
          height={400}
          rowHeight={35}
          rowKey="id"
          showRowNum={true}
          textWrap={{
            enabled: true,
            lineClamp: 3
          }}
        />
      </div>
    </div>
  );
}
```
