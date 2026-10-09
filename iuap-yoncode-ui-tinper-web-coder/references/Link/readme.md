---
tags:
  - TinperNextPro
  - Link组件
---
# Link 超链接

<!--Link-->

## API

- 属性如下：

| 参数               | 说明                                               | 类型                                                   | 默认值 | 版本    |
| ------------------ | -------------------------------------------------- | ------------------------------------------------------ | ------ | ------- |
| browser            | 是否是浏览态                                       | boolean                                                | false  | 15.11.x |
| fieldid            | fieldid                                            | string                                                 | -      | 1.0.9   |
| className          | 类名                                               | string                                                 | -      | 1.0.9   |
| style              | 根元素样式                                         | React.CSSProperties                                    | -      | 1.0.9   |
| contentStyle       | 内容区样式                                         | React.CSSProperties                                    | -      | 1.0.9   |
| bordered           | 设置边框，支持无边框、下划线模式                   | boolean/bottom                                         | true   | 1.0.9   |
| disabled           | 禁用                                               | boolean                                                | -      | 1.0.9   |
| readOnly           | 只读                                               | boolean                                                | -      | 1.0.9   |
| allowClear         | 是否显示清空按钮                                   | boolean                                                | true   | 1.0.9   |
| hideText           | 是否显示文本输入框                                 | boolean                                                | -      | 1.0.9   |
| requiredStyle      | 必填样式                                           | boolean                                                | -      | 1.0.9   |
| addressPlaceholder | 网址占位符                                         | string                                                 | -      | 1.0.9   |
| textPlaceholder    | 文本占位符                                         | string                                                 | -      | 1.0.9   |
| defaultAddress     | 网址默认值                                         | string                                                 | -      | 1.0.9   |
| defaultText        | 文本默认值                                         | string                                                 | -      | 1.0.9   |
| tips               | 下方提示文字                                       | ReactNode                                              | -      | 1.0.9   |
| check              | 是否开启校验                                       | boolean                                                | true   | 1.0.9   |
| pattern            | 检验正则                                           | RegExp                                                 | -      | 1.0.9   |
| required           | 是否必填                                           | boolean                                                | -      | 1.0.9   |
| customCheck        | 自定义校验规则，返回 true 检验成果，false 校验失败 | (address: string) => boolean                           | -      | 1.0.9   |
| value              | 链接地址及文本                                     | {linkAddress: string, linkText: string}                | -      | 1.0.9   |
| onClick            | 预览态点击文本回调                                 | (val) => void                                          | -      | 1.0.9   |
| onFocus            | 输入框聚焦回调                                     | (e, type, value) => void                               | -      | 15.3.9  |
| onBlur             | 输入框失焦回调                                     | (e, type, value) => void                               | -      | 15.3.9  |
| onAddressChange    | 链接地址变化回调                                   | (val) => void                                          | -      | 1.0.9   |
| onChange           | 链接地址或文本变化回调                             | (val) => void                                          | -      | 1.0.9   |
| onError            | 校验失败回调                                       | (val: string, type: string, validateRule: any) => void | -      | 1.0.9   |
| onSuccess          | 检验成功回调                                       | (val: string) => void                                  | -      | 1.0.9   |
| maxTextLength      | 文本最多输入长度                                   | number                                                 | 50     | 1.0.9   |
