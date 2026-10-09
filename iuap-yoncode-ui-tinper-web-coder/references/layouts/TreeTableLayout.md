# TreeTableLayout

`TreeTableLayout` 是左树右内容布局组件，适用于左侧分类树、组织树、目录树，右侧展示表格或卡片内容的页面。

## 导入方式

```tsx
import { TreeTableLayout } from 'tne-tinpernextpro-fe/layouts';
```

## Props

| 参数 | 类型 | 必填 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| `tree` | `ReactNode` | 是 | - | 左侧树区域 |
| `content` | `ReactNode` | 是 | - | 右侧内容区域 |
| `treeWidth` | `number \| string` | 否 | `240` | 左侧树宽度，number 会转成 px |
| `contentKind` | `'table' \| 'card'` | 否 | `'table'` | 右侧内容类型 |
| `className` | `string` | 否 | - | 自定义类名 |

## 示例

```tsx
<TreeTableLayout
  tree={
    <Tree
      treeData={treeData}
      selectedKeys={selectedKeys}
      onSelect={handleSelectTree}
    />
  }
  content={
    <DataGrid
      rowKey="id"
      data={rows}
      columnDefs={columns}
      pagination={pagination}
    />
  }
  treeWidth={280}
  contentKind="table"
/>
```

## 使用建议

- 右侧是表格时 `contentKind="table"`；右侧是卡片列表或详情卡片时用 `contentKind="card"`。
- `treeWidth` 可以传数字或 CSS 宽度字符串，例如 `280`、`'22%'`、`'18rem'`。
- 左侧树组件可用 Base `Tree`、`TreeSelect` 的面板形态或业务自定义树。
- 右侧表格选型仍按 `rules/selection-rules.md`，新建业务列表优先 `DataGrid`。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/TreeTableLayout.tsx`
