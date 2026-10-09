# 其他已知问题

## Typography 只有 Paragraph，没有 Title 和 Text

**问题**: `Typography` 只导出了 `Typography.Paragraph`，**不存在** `Typography.Title` 和 `Typography.Text`。
**影响**: 使用 `<Typography.Title>` 或 `<Typography.Text>` 会在运行时报错（组件为 undefined）。
**方案**: 用原生 HTML 标签替代：
```tsx
// ✅ 正确
import { Typography } from '@tinper/next-ui'
<Typography.Paragraph ellipsis>长文本...</Typography.Paragraph>
<h1 style={{ fontSize: 24, fontWeight: 700 }}>标题</h1>

// ❌ 错误 — 不存在
<Typography.Title level={1}>标题</Typography.Title>
<Typography.Text>文本</Typography.Text>
```

## Carousel 没有 autoplaySpeed 属性

`Carousel` 的 `autoplay` 是 boolean 类型，控制是否自动播放。内部透传给 `react-slick`，`autoplaySpeed` 可能被消费但不是官方 API。

## Timeline 不支持 items 属性

只能用 `<Timeline.Item>` 子组件模式：
```tsx
// ✅ 正确
<Timeline>
  <Timeline.Item color="blue">步骤一</Timeline.Item>
  <Timeline.Item>步骤二</Timeline.Item>
</Timeline>

// ❌ 错误
<Timeline items={[{ children: '步骤一', color: 'blue' }]} />
```

## Select showSearch / filterOption 类型缺失

运行时有效但 TypeScript 类型未声明，需 `@ts-ignore` 或自行扩展类型声明。

## DatePicker 使用 Moment 而非 Dayjs

`DatePicker` 内部使用 **Moment.js**。`value` 接受 `Moment | string | null`，`onChange` 返回 Moment 对象。
```tsx
import moment from 'moment'

// ✅ 正确
<DatePicker value={moment('2024-06-12')} onChange={(m) => m?.format('YYYY-MM-DD')} />

// ❌ 错误 — Dayjs 对象会导致静默失败
import dayjs from 'dayjs'
<DatePicker value={dayjs('2024-06-12')} />
```

## Modal maskClosable 默认值与 antd 不同

TinperNext Modal 的 `maskClosable` 默认为 **`false`**（antd 默认 `true`）。点击蒙层默认不会关闭弹窗。

## visible vs show

Modal、Drawer 等组件同时支持 `visible` 和 `show`，源码逻辑 `visible` 优先。新代码统一用 `visible`。

**Drawer 陷阱**: Drawer 的处理逻辑是 `show: visible ? visible : show`，即 `visible=false` 时会 fallback 到 `show` 的值。如果同时传了 `show={true}` 和 `visible={false}`，抽屉**不会关闭**。解决：不要混用，只用 `visible`。

## EditTable rowKey 必须是 string

**问题**: EditTable 的 `rowKey` 只接受 `string` 类型，传入函数会直接抛出 `Error('传入 rowKey 不符合格式, 请调整为 string 格式')`。这与 Base Table（支持 `string | function`）不同。
```tsx
// ✅ 正确
<EditTable rowKey="id" />

// ❌ 报错
<EditTable rowKey={(record) => record.id} />
```

## EditTable 自定义编辑组件必须消费 value/onChange

EditTable 列配置中使用 `renderFormItem` 返回自定义编辑组件时，该组件必须接受并消费 `value` 和 `onChange` props，否则单元格编辑后取值为空：
```tsx
columns={[{
  dataIndex: 'custom',
  editType: 'custom',
  renderFormItem: (text, record, index) => (
    // 必须透传 value 和 onChange
    <MyInput value={text} onChange={(val) => { /* EditTable 内部会注入 onChange */ }} />
  ),
}]}
```

## DataTable 属性名是 data 不是 dataSource

DataTable / Table 传入数据的属性名是 `data`，不是 `dataSource`。写成 `dataSource` 不会报错但数据不渲染：
```tsx
// ✅ 正确
<DataTable data={list} columns={columns} />

// ❌ 无数据渲染，且不报错
<DataTable dataSource={list} columns={columns} />
```

> Base Table 源码中两者都接受（`dataSource || data || []`，`dataSource` 优先），但 DataTable 只认 `data`。统一用 `data` 最安全。

## DataTable isSort / isBigData 默认关闭

`isSort` 和 `isBigData` 默认值都是 **`false`**，需要显式开启：
```tsx
<DataTable isSort isBigData columns={columns} request={fetchData} />
```
`isDragColumn` 默认 `true`（列宽拖拽默认开启）。

## DataForm options vs EditTable editOptions

DataForm.Item 传选项用 `options`（平铺），EditTable 列配置传选项用 `editOptions`（对象包裹）。两者不能混用：
```tsx
// DataForm.Item — 直接传 options
<DataForm.Item inputType="select" options={[{ label: 'A', value: '1' }]} />

// EditTable 列配置 — 用 editOptions 包裹
{ editType: 'select', editOptions: { options: [{ label: 'A', value: '1' }] } }
```

## EditGrid rowKey 支持 string 或函数

`EditGrid` 的 `rowKey` 支持 `string` 类型或 `(record) => string` 函数，默认值为 `'id'`。
```tsx
// ✅ 字符串
<EditGrid rowKey="id" />

// ✅ 函数
<EditGrid rowKey={(record) => record.id} />
```

## Popconfirm onConfirm 已废弃，用 onClose

**问题**: antd 习惯用 `onConfirm`，但 TinperNext 中 `onConfirm` 已废弃（源码中标注 `~~onConfirm~~`）。
**方案**: 确认按钮回调统一用 `onClose`：
```tsx
// ✅ 正确
<Popconfirm content="确定删除？" onClose={handleDelete}>
  <Button>删除</Button>
</Popconfirm>

// ❌ 废弃
<Popconfirm onConfirm={handleDelete}>...</Popconfirm>
```

## Popconfirm content 和 description 是同一个位置

`content` 和 `description` 渲染到同一个 DOM 位置（`content` 优先），`title` 才是标题区域。与 antd（`title` 是主文案）不同：
```tsx
// TinperNext — content 是主文案，title 是上方标题
<Popconfirm title="删除确认" content="此操作不可逆" />

// antd — title 是主文案，description 是补充
// <Popconfirm title="此操作不可逆" description="删除后无法恢复" />
```

## Alert type 和 colors 优先级

`type` 优先于 `colors`。`type` 支持 `"error"`（自动映射为 `danger`），`colors` 不支持 `"error"`：
```tsx
// ✅ 推荐
<Alert type="error" closable={false}>错误提示</Alert>

// ❌ 不生效
<Alert colors="error">...</Alert>  // error 不在 colors 取值范围内
```

## Alert closable 默认 true，但真实项目几乎都关闭

源码默认 `closable={true}`，但企业场景下提示条通常不允许关闭。建议显式传 `closable={false}`。

## Form.createForm validateFields 支持回调和 Promise 两种风格

HOC 式 `Form.createForm()` 的 `validateFields` 同时支持回调和 Promise：
```tsx
// 回调风格（旧项目常见）
this.props.form.validateFields((errors, values) => {
  if (errors) return;
  submit(values);
});

// Promise 风格（不传回调则返回 Promise）
this.props.form.validateFields().then(values => submit(values));
```
Hook 式 `Form.useForm()` 和 Ref 式只支持 Promise 风格。迁移旧代码时注意去掉回调参数。
