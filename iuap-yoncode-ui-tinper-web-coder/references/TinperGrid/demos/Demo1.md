---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 自适应行高
展示如何根据单元格内容自动调整行高

```jsx
import React, { useState, useCallback } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';
import { RowStyleModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowstyle';
import { RowHoverModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rowhover';
import { Button } from '@tinper/next-ui';

ModuleRegistry.registerModules([RowNumbersModule, RowStyleModule, RowHoverModule]);

/**
 * 自适应行高示例
 * 展示如何根据单元格内容自动调整行高
 */
export default function AutoRowHeightExample() {
  // 控制自定义组件是否高度翻倍
  const [isExpanded, setIsExpanded] = useState(false);

  // 使用 useCallback 保持 data 引用稳定，但内容会随 isExpanded 变化
  const data = React.useMemo(() => [
    {
      id: 1,
      name: '张三',
      description: '这是一段简短的描述',
      content: '正常内容',
      // 自定义单元格数据 - 自定义组件
      custom: {
        type: 'component',
        title: '组件标题',
        text: '这是一个自定义组件，包含标题和内容文字。这里可以放置较多的文字内容来测试行高自适应效果。',
        hasImage: true,
        extraContent: isExpanded ? '这是展开后的额外内容，用来测试当内容增加时，行高是否能正确自适应。' : ''
      }
    },
    {
      id: 2,
      name: '李四',
      description: '这是一段很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长的描述文本，需要换行显示',
      content: '这也是一段很长的内容，包含了很多信息，需要多行来展示。这样可以更好地展示自适应行高的效果。',
      custom: {
        type: 'component',
        title: '复杂组件',
        text: '这是一个自定义组件，包含多个元素。这里有标题、副本和按钮，可以测试复杂内容的行高自适应。',
        hasButton: true,
        extraContent: isExpanded ? '这是一段额外的扩展内容，用来测试行高自动调整。当内容增加时，表格行高应该自动撑开以适应内容。' : ''
      }
    },
    {
      id: 3,
      name: '王五',
      description: '中等长度的描述文本，大概需要两到三行来显示',
      content: '普通内容',
      custom: {
        type: 'component',
        title: '带图标的组件',
        text: '这是一个带图标的自定义组件，可以测试不同类型内容的行高测量。',
        hasImage: true,
        extraContent: isExpanded ? '这是第二段内容，用来增加高度。' : ''
      }
    },
    {
      id: 4,
      name: '赵六',
      description: '短描述',
      content: '超级长的内容文本，包含大量信息。在实际业务场景中，这种情况很常见，比如用户评论、商品描述，文章摘要等等。自适应行高可以确保所有内容都能完整显示，而不会被截断。',
      custom: {
        type: 'component',
        title: '长文本组件',
        text: '这是一段较长的文本内容，用来测试当单元格包含大量文字时，行高是否能正确撑开。',
        extraContent: isExpanded ? '这是第二段内容，用来增加高度。第三段内容继续增加，以便更好地测试行高自适应功能。' : ''
      }
    },
    {
      id: 5,
      name: '孙七',
      description: '正常的描述文本',
      content: '短内容',
      custom: {
        type: 'component',
        title: '简单组件',
        text: '这是一个简单的自定义组件',
        extraContent: isExpanded ? '这是展开后的额外内容。' : ''
      }
    },
  ], [isExpanded]);

  // 切换展开状态的处理函数
  const handleToggleExpand = useCallback(() => {
    setIsExpanded(prev => !prev);
  }, []);

  // 自定义单元格渲染器 - 统一使用组件类型
  // eslint-disable-next-line react/display-name
  const CustomCellRenderer = (props: any) => {
    const { value } = props;
    if (!value || value.type !== 'component') return null;

    return (
      <div style={{
        padding: '8px',
        background: '#f5f5f5',
        borderRadius: '4px',
      }}>
        {/* 标题 */}
        {value.title && (
          <div style={{ fontWeight: 'bold', marginBottom: '8px', color: '#1890ff' }}>
            {value.title}
          </div>
        )}

        {/* 图标占位 */}
        {value.hasImage && (
          <div style={{
            width: '100%',
            height: '60px',
            background: '#e6f7ff',
            borderRadius: '4px',
            marginBottom: '8px',
            display: 'flex',
            alignItems: 'center',
            justifyContent: 'center',
            color: '#1890ff',
            border: '1px dashed #1890ff'
          }}>
            <span>🖼️ 图片占位区域</span>
          </div>
        )}

        {/* 内容文本 */}
        <div style={{ marginBottom: '8px', color: '#333' }}>
          {value.text}
        </div>

        {/* 额外内容 */}
        {value.extraContent && (
          <div style={{
            marginTop: '8px',
            padding: '8px',
            background: '#e6f7ff',
            borderRadius: '4px',
            border: '1px solid #91d5ff',
            color: '#333'
          }}>
            {value.extraContent}
          </div>
        )}

        {/* 按钮 */}
        {value.hasButton && (
          <button
            style={{
              marginTop: '8px',
              padding: '4px 12px',
              background: '#1890ff',
              color: 'white',
              border: 'none',
              borderRadius: '4px',
              cursor: 'pointer'
            }}
            onClick={() => console.log('点击了按钮')}
          >
            操作按钮
          </button>
        )}
      </div>
    );
  };

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
    {
      field: 'custom',
      headerName: '自定义单元格',
      width: 280,
      // eslint-disable-next-line react/display-name
      render: (value: any) => <CustomCellRenderer value={value} />,
    },
  ];

  return (
    <div style={{ padding: '20px' }}>
      <h2>自适应行高示例</h2>
      <p>表格会根据"描述"、"内容"和"自定义单元格"列的内容自动调整行高</p>

      <div style={{ marginBottom: '16px' }}>
        <Button
          colors={isExpanded ? 'primary' : 'default'}
          onClick={handleToggleExpand}
        >
          {isExpanded ? '收起扩展内容' : '展开扩展内容 (测试行高自适应)'}
        </Button>
        <span style={{ marginLeft: '12px', color: '#666', fontSize: '14px' }}>
          当前状态: {isExpanded ? '已展开' : '未展开'}
        </span>
      </div>

      <div style={{ marginTop: '20px' }}>
        <Grid
          data={data}
          columnDefs={columnDefs}
          height={400}
          rowHeight={35}
          rowKey="id"
          showRowNum={true}
          // 启用文字换行（已移除 autoRowHeight 联动，需要手动开启）
          textWrap={{
            enabled: true,
            columns: ['description', 'content', 'custom']
          }}
          // 启用自适应行高 - 测量description、content和custom列
          autoRowHeight={{
            enabled: true,
            columns: ['description', 'content', 'custom'],  // 测量包含自定义单元格的这列
            minHeight: 35,    // 最小行高
            maxHeight: 200,   // 最大行高
            defaultHeight: 35 // 默认行高
          }}
          // 行悬浮操作按钮
          rowHover={{
            position: 'right',
            offset: 10,
            rowHoverContent: ({ rowKey, rowIndex, rowData }) => (
              <div
                style={{
                  display: 'flex',
                  gap: 8,
                  height: '100%',
                  justifyContent: 'center',
                  alignItems: 'center',
                  padding: '4px 8px',
                }}
              >
                <Button
                  size="small"
                  colors="dark"
                  onClick={(e) => {
                    e.stopPropagation();
                    console.log('查看', rowData);
                  }}
                >
                  查看
                </Button>
                <Button
                  size="small"
                  colors="dark"
                  onClick={(e) => {
                    e.stopPropagation();
                    console.log('编辑', rowData);
                  }}
                >
                  编辑
                </Button>
              </div>
            ),
          }}
        />
      </div>
    </div>
  );
}
```
