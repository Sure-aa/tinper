# NextPro Layouts 总览

Layouts 是 `tne-tinpernextpro-fe/layouts` 导出的页面结构组件，用于统一列表页、详情页、页签区、工具栏和左树右内容布局。它们不是 `@tinper/next-ui Layout` 的替代品，而是 NextPro 业务页面布局外壳。

## 导入方式

```tsx
import {
  DetailLayout,
  LineTabs,
  ListLayout,
  ToolbarLayout,
  TreeTableLayout,
} from 'tne-tinpernextpro-fe/layouts';
```

## 组件索引

| 组件 | 说明 | 文档 |
| --- | --- | --- |
| `ListLayout` | 列表页布局容器，子组件流式平铺 | `./ListLayout.md` |
| `DetailLayout` | 详情页布局容器，带 `Header` / `Footer` 静态子组件 | `./DetailLayout.md` |
| `LineTabs` | 基于 TinperNext `Tabs` 的 fill-line 子表页签 | `./LineTabs.md` |
| `ToolbarLayout` | 工具栏布局，支持左、中、右、两端对齐 | `./ToolbarLayout.md` |
| `TreeTableLayout` | 左树右表或左树右卡片布局 | `./TreeTableLayout.md` |

## 使用建议

- 列表页主容器用 `ListLayout`，查询区、工具栏、表格自然顺序放入。
- 详情页主容器用 `DetailLayout`，顶部信息放 `DetailLayout.Header`，底部操作放 `DetailLayout.Footer`。
- 子表页签优先用 `LineTabs`，内容仍用 `DataGrid`、`EditGrid`、`DataTable` 等业务表格。
- 左树右内容页优先用 `TreeTableLayout`，`contentKind` 按右侧内容选择 `table` 或 `card`。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/layouts/ListLayout.tsx`
- `node_modules/tne-tinpernextpro-fe/src/layouts/DetailLayout.tsx`
- `node_modules/tne-tinpernextpro-fe/src/layouts/LineTabs.tsx`
- `node_modules/tne-tinpernextpro-fe/src/layouts/ToolbarLayout.tsx`
- `node_modules/tne-tinpernextpro-fe/src/layouts/TreeTableLayout.tsx`
