# 与 antd 的 API 差异

以下基于源码验证，标注 TinperNext 与 antd 类 API 的差异。

## 不支持的 API

| 组件 | 属性 | 说明 |
| --- | --- | --- |
| Timeline | `items` 属性 | 只支持 `<Timeline.Item>` 子组件模式，不支持 antd v5 风格的 `items` 数组 |
| Typography | `.Title` / `.Text` | 只有 `.Paragraph`，标题用 `<h1>`-`<h6>`，文本用 `<span>` |
| Carousel | `autoplaySpeed` | 只有 `autoplay`（boolean），速度控制可尝试透传但不保证生效 |
| Popconfirm | `onConfirm` | 已废弃，确认回调用 `onClose` |

## 运行时有效但类型缺失

| 组件 | 属性 | 说明 |
| --- | --- | --- |
| Select | `showSearch` / `filterOption` | 运行时透传给 `@tinper/rc-select`，功能正常，但 TypeScript 类型未声明，需 `@ts-ignore` |
| Breadcrumb | `Breadcrumb.Item` | 运行时有效，但 TypeScript 类型可能缺失 |

## 行为差异

| 组件 | 属性 | 差异说明 |
| --- | --- | --- |
| DatePicker | `value` 类型 | 接受 `Moment | string | null`，**不是 Dayjs**。不要传 Dayjs 对象，会静默失败 |
| Message | 方法列表 | 多了 `infolight/successlight/dangerlight/warninglight` 独有方法；`error` 内部映射为 `danger` 颜色 |
| Message | 调用参数 | 支持 `{ content, message, duration, onClose }`，`message` 和 `content` 都接受，`message` 优先 |
| Table | `rowSelection` | 存在新旧两套 API 路径，新 API（推荐）与 antd 一致，旧 API 用 `_checked`/`_disabled` 字段 |
| Modal | `maskClosable` | 声明式 `<Modal>` 默认 `false`（antd 默认 true），点击蒙层默认不关闭。但命令式 `Modal.confirm()` 等走废弃属性 `backdropClosable` 默认 `true`，即命令式弹窗点蒙层默认会关闭——若要防误关需显式传 `maskClosable: false` |
| Alert | `type` vs `colors` | 两个属性都接受，`type` 优先。`type` 多支持 `"error"`（→ `danger`），`colors` 不接受 `"error"` |
| Alert | `closable` 默认值 | 默认 `true`（antd 默认 `false`），真实项目几乎都显式传 `closable={false}` |
| Popconfirm | 确认回调 | `onConfirm` 已废弃 → 用 `onClose`；确认消息用 `content`（非 antd 的 `title`） |
| Tag | `color` 命名色 | 多了 `half-blue/half-green/half-red/half-yellow/half-dark` 半透明系列和 `invalid/start` 语义色 |

## 完全兼容的 API

| 组件 | 属性 | 说明 |
| --- | --- | --- |
| Table | `rowSelection.type/selectedRowKeys/onChange` | 完整支持 |
| Table | `footer` | 无差异 |
| Form | `Form.useForm()` | 基于 rc-field-form，与 antd v4 一致 |
| Steps | `items` 属性 | `items` 和 `Steps.Step` 子组件两种都支持 |
| Menu | `items` + `mode="horizontal"` | 无差异 |
| InputNumber | `precision` | 完整支持 |
| Progress | `strokeColor` 渐变 | 支持 `{ from, to, direction }` 对象 |
