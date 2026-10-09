# DetailLayout

`DetailLayout` 是详情页布局容器，提供 `DetailLayout.Header` 和 `DetailLayout.Footer` 静态子组件，用于组织顶部信息、主体表单和底部操作区。

## 导入方式

```tsx
import { DetailLayout } from 'tne-tinpernextpro-fe/layouts';
```

## Props

### DetailLayout

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `children` | `ReactNode` | 是 | 详情页内容 |

### DetailLayout.Header

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `children` | `ReactNode` | 是 | 详情页头部内容 |

### DetailLayout.Footer

| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `children` | `ReactNode` | 是 | 详情页底部操作内容 |

## 示例

```tsx
<DetailLayout>
  <DetailLayout.Header>
    <h2>销售订单</h2>
    <Tag size="sm" color="success">已保存</Tag>
  </DetailLayout.Header>

  <DataForm ref={formRef} formMode={formMode} formLayout={3}>
    <DataForm.Item name="code" label="编码" inputType="input" />
    <DataForm.Item name="name" label="名称" inputType="input" required />
  </DataForm>

  <DetailLayout.Footer>
    <ToolbarLayout>
      <Button onClick={handleCancel}>取消</Button>
      <Button colors="primary" onClick={handleSave}>保存</Button>
    </ToolbarLayout>
  </DetailLayout.Footer>
</DetailLayout>
```

## 使用建议

- `DetailLayout.Header` 适合放标题、状态、摘要操作。
- `DetailLayout.Footer` 适合放保存、取消、提交等底部操作。
- 表单仍优先用 `DataForm`，简单少字段场景可用 Base `Form`。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/DetailLayout.tsx`
