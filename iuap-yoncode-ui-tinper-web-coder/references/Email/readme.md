---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

<!--Email-->
## API

- 属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| placeholder     | 提示信息               | string               | you@example.com          | 1.0.9  |
| className     | 类名               | string               |      -      | 1.0.9  |
| style     | 根元素样式               | React.CSSProperties               |     -       | 1.0.9  |
| selectStyle     | select 元素样式               | React.CSSProperties               |      -      | 1.0.9  |
| bordered     | 设置边框，支持无边框、下划线模式               | boolean/bottom               | true         | 1.0.9  |
| disabled     | 禁用               | boolean               | false         | 1.0.9  |
| readOnly     | 只读               | boolean               | false         | -  |
| notFound     | 当下拉列表为空时显示的内容               | ReactNode               | 暂无数据～      | 1.0.9  |
| onChange     | 邮箱号变化回调               | (val: string, boo: boolean) => void               | -      | 1.0.9  |
| value     | 邮箱号内容               | string               | -      | 1.0.9  |
| tips     | 下方提示文字               | ReactNode               | -      | 1.0.9  |
| allowClear     | 是否显示清空按钮               | boolean               | true      | 1.0.9  |
| check     | 是否开启校验               | boolean               | false      | 1.0.9  |
| pattern     | 检验正则               | RegExp               | -      | 1.0.9  |
| required     | 是否必填               | boolean               | false      | 1.0.9  |
| customCheck     | 自定义校验规则，返回 true 检验成果，false 校验失败               | (val: string) => boolean               | -      | 1.0.9  |
| onError     | 校验失败回调               | (val: string, pattern: RegExp) => void             | -      | 1.0.9  |
| onSuccess     | 检验成功回调               | (val: string) => void             | -      | 1.0.9  |
| onClear     | 点击清空回调               | () => void             | -      | 1.0.9  |
| maxLength     | @字符之前最多输入长度               | number             | 20      | 1.0.9  |
| emailDomainList     | 可选邮箱类型               | 参照 emailDomainListDefault             | emailDomainListDefault      | 1.0.9  |
| locale     | 语言               | string         | zh-cn      | 1.0.9  |
| onMouseEnter     | 鼠标移入时回调               | function         | -      | 1.0.9  |
| onMouseLeave     | 鼠标移出时回调               | function         | -      | 1.0.9  |
| selectProps     | 传给下拉框的其他属性            | {}        | -         | 1.0.9  |
| onFocus     | 下拉框聚焦回调            | function        | -         | -  |
| onBlur     | 下拉框失焦回调            | function        | -         | -  |
| browser     | 是否开启浏览态            | boolean        | false         | -  |
| browserClassName     | 浏览态类名            | string        | -         | -  |
| browserStyle     | 浏览态样式           | CSSProperties        | -         | -  |

### 类型说明

```js
emailDomainListDefault = ['yonyou.com', '163.com', 'qq.com', 'gmail.com', 'yahoo.com', 'msn.com', 'hotmail.com', 'aol.com', 'ask.com', 'live.com', '0355.net', '126.com', 'outlook.com']
```

### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | `${fieldid}_email` | 1.0.9  |
| 下拉框 | `${fieldid}_email_select` | 1.0.9  |