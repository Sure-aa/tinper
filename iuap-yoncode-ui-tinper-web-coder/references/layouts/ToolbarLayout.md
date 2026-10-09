# ToolbarLayout

`ToolbarLayout` 是工具栏布局组件，用于统一按钮组和批量操作区域的对齐方式。

## 导入方式

```tsx
import { ToolbarLayout } from 'tne-tinpernextpro-fe/layouts';
```

## Props

| 参数 | 类型 | 必填 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| `children` | `ReactNode` | 是 | - | 工具栏内容 |
| `align` | `'left' \| 'center' \| 'right' \| 'between'` | 否 | `'right'` | 对齐方式 |
| `className` | `string` | 否 | - | 自定义类名 |

## 示例

```tsx
<ToolbarLayout align="between">
  <Space>
    <Button onClick={handleBatchDelete}>删除</Button>
    <Button onClick={handlePrint}>打印</Button>
  </Space>
  <Button colors="primary" onClick={handleCreate}>新增</Button>
</ToolbarLayout>
```

## 对齐选择

| 场景 | align |
| --- | --- |
| 右侧新增、保存等主操作 | `right` |
| 左侧批量操作 | `left` |
| 左右两组操作 | `between` |
| 少见的居中动作区 | `center` |

## 使用建议

- 按钮间距用 `Space` 或组件库按钮组处理，不要在按钮上手写零散 margin。
- 列表页工具栏通常放在 `SearchForm` 和表格之间。
- 详情页底部操作可放在 `DetailLayout.Footer` 内。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/ToolbarLayout.tsx`
