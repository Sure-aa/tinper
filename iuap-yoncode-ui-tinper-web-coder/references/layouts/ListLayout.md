# ListLayout

`ListLayout` 是列表页布局容器，负责提供统一的列表页外壳。子组件按传入顺序流式平铺，通常用于查询区、工具栏、表格和分页区域的组合。

## 导入方式

```tsx
import { ListLayout } from 'tne-tinpernextpro-fe/layouts';
```

## Props

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `children` | `ReactNode` | 是 | 列表页内部内容 |

## 示例

```tsx
<ListLayout>
  <SearchForm ref={searchRef} onSearch={reload} onReset={reload}>
    <SearchForm.Item name="name" label="名称" inputType="input" />
  </SearchForm>

  <ToolbarLayout>
    <Button colors="primary" onClick={handleCreate}>新增</Button>
  </ToolbarLayout>

  <DataGrid
    rowKey="id"
    data={rows}
    columnDefs={columns}
    pagination={pagination}
  />
</ListLayout>
```

## 使用建议

- `ListLayout` 只负责外层结构，不替代表格、查询表单或工具栏。
- 工具栏区域建议搭配 `ToolbarLayout`。
- 表格选型仍先走 `rules/selection-rules.md` 的表格决策。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/ListLayout.tsx`
