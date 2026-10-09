---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

<!--Phone-->
## API

- 属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| className     | 根元素类名               | string               | -          | 1.0.9  |
| style     | 根元素样式               | React.CSSProperties               | -          | 1.0.9  |
| domesticSource     | 国内区号设置，不设置时走默认内置的国际区号    | domesticSourceType               | -          | 1.0.9  |
| bordered     | 设置边框，支持无边框、下划线模式               | boolean/bottom               | true         | 1.0.9  |
| disabled     | 禁用              | boolean             | false        | 1.0.9  |
| readOnly     | 只读              | boolean             | false        | -  |
| onCityCodeSelect     | 国内区号切换时回调函数              | (cityCode: string) => void             | -        | 1.0.9  |
| placeholder     | 输入框提示信息，H表示主机号，E表示分机号              | {H: string, E: string}            | -        | 1.0.9  |
| onChange     | 输入内容变化回调            | (value: {H: string, E: string}, type: 'H' / 'E' / 'cityCode', cityCode: string) => void            | -        | 1.0.9  |
| onFocus     | 聚焦回调函数            | (value: {H: string, E: string}, type: 'H' / 'E' / 'cityCode', cityCode: string) => void            | -        | 1.0.9  |
| onBlur     | 失焦回调函数            | (value: {H: string, E: string}, type: 'H' / 'E' / 'cityCode', cityCode: string) => void            | -        | 1.0.9  |
| validate     | 输入限制            | function        | -        | 1.0.9  |
| noExtension     | 不显示分机号            | boolean        | true        | 1.0.9  |
| hideCityCode     | 隐藏国内区号            | boolean        | false        | 1.0.9  |
| check     | 是否开启默认校验            | boolean        | true        | 1.0.9  |
| required     | 必填检验            | boolean        | false        | 1.0.9  |
| onError     | 校验失败回调            | ({value: {H: string, E: string}, cityCode: string}, tag: string) => void            | -        | 1.0.9  |
| onSuccess     | 校验成功回调            | ({value: {H: string, E: string}, cityCode: string}) => void            | -        | 1.0.9  |
| regH     | 主机号校验            | RegExp            | /\d{7,8}$/        | 1.0.9  |
| regE     | 分机号校验            | RegExp            | /^\d{3,4}$/        | 1.0.9  |
| value     | 输入框值              | {H: string, E: string}            | -        | 1.0.9  |
| firstMaxLength     | 主机号最大长度              | number            | -        | 1.0.9  |
| lastMaxLength     | 分机号最大长度              | number            | -        | 1.0.9  |
| focus     | 是否聚焦到第一个输入框              | boolean            | false        | 1.0.9  |
| inputProps     | 传给输入框的其他属性            | {}        | -         | 1.0.9  |
| selectProps     | 传给下拉框的其他属性            | {}        | -         | 1.0.9  |
| swapOrder     | 是否切换主机号分机号位置，仅在显示分机号时适用            | boolean       | false         | -  |
| cityCode     | 显示区号            | string       | -         | -  |
| editable     | 设置为 false 时，区域选择无法打开            | boolean       | true         | -  |
| browser     | 是否开启浏览态            | boolean       | false         | -  |
| browserStyle     | 浏览态样式            | CSSProperties       | -         | -  |
| browserClassName     | 浏览态类名            | string       | -         | -  |
| customRender     | 浏览态显示内容，设置此值后，将不解析任何传入的值，只显示此函数返回值            | fun       | -         | -  |


### 类型说明

```js
interface domesticSourceType {
  cityName: string;
  code: string;
  // 可选属性
  [key: string]: any; // 允许其他任意属性
}
```

### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | `${fieldid}_phone` | 1.0.9  |
| 下拉框 | `${fieldid}_phone_select` | 1.0.9  |
| 主输入框 | `${fieldid}_phone_first` | 1.0.9  |
| 分输入框 | `${fieldid}_phone_second` | 1.0.9  |
