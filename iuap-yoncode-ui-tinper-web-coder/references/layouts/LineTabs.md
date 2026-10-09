# LineTabs

`LineTabs` 是基于 `@tinper/next-ui Tabs` 的 fill-line 页签组件，常用于详情页子表、分组内容和明细区域切换。

## 导入方式

```tsx
import { LineTabs } from 'tne-tinpernextpro-fe/layouts';
```

## Props

| 参数 | 类型 | 必填 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| `children` | `ReactNode` | 否 | - | 未传 `items` 时作为默认单页签内容 |
| `items` | `LineTabItem[]` | 否 | - | 多页签配置 |
| `tabTitle` | `ReactNode` | 否 | `'子表'` | 默认单页签标题 |
| `defaultActiveKey` | `string` | 否 | 第一项 key | 默认激活页签 |
| `activeKey` | `string` | 否 | - | 受控激活页签 |
| `extra` | `ReactNode` | 否 | - | 页签右侧额外内容 |
| `className` | `string` | 否 | - | 自定义类名 |
| `fieldid` | `string` | 否 | - | 自动化标识 |
| `onChange` | `(activeKey: string) => void` | 否 | - | 页签切换回调 |

### LineTabItem

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `key` | `string` | 是 | 页签 key |
| `title` | `ReactNode` | 是 | 页签标题 |
| `content` | `ReactNode` | 是 | 页签内容 |

## 示例

```tsx
<LineTabs
  items={[
    {
      key: 'items',
      title: '明细',
      content: <EditGrid rowKey="id" data={items} columnDefs={itemColumns} />,
    },
    {
      key: 'logs',
      title: '日志',
      content: <DataGrid rowKey="id" data={logs} columnDefs={logColumns} />,
    },
  ]}
  extra={<Button size="sm" onClick={handleAddLine}>增行</Button>}
  onChange={setActiveTab}
/>
```

## 使用建议

- 只有一个子表时可直接传 `children`，用 `tabTitle` 修改标题。
- 多个子区域时使用 `items`，不要同时依赖 `children` 作为额外页签。
- `extra` 适合放增行、刷新等页签级操作。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/layouts/LineTabs.tsx`
