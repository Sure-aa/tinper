---
tags:
  - TinperNextPro
  - Mobile组件
---
# Mobile 手机号

<!--Mobile-->
## API

- 属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| placeholder     | 提示信息               | string               | -          | 1.0.9  |
| className     | 类名设置               | string               | -          | 1.0.9  |
| countryList     | 国际区号列表，不设置时走默认内置国际区号              | countryListType               | -         | 1.0.9  |
| style     | 自定义样式              | React.CSSProperties             | -         | 1.0.9  |
| disabled     | 禁用              | boolean             | false        | 1.0.9  |
| readOnly     | 只读              | boolean             | false        | -  |
| bordered     | 设置边框，支持无边框、下划线模式               | boolean/bottom               | true         | 1.0.9  |
| onFocus     | 聚焦回调              | (value, country_code, country) => void             | -         | 1.0.9  |
| onChange     | 内容变化回调              | (value, country_code, country) => void             | -         | 1.0.9  |
| onBlur     | 失焦回调              | (value, country_code, country) => void             | -         | 1.0.9  |
| iconRender     | 输入框后缀              | ReactNode             | -         | 1.0.9  |
| onCountryChange     | 区号变化回调              | (country_locale, country_code, country, mobile) => void        | -         | 1.0.9  |
| onKeyDown     | 键盘事件回调（Tab键、方向键、回车键）            | ({country_code, country, mobile}) => void        | -         | 1.0.9  |
| inputProps     | 传给输入框的其他属性            | {}        | -         | 1.0.9  |
| selectProps     | 传给下拉框的其他属性            | {}        | -         | 1.0.9  |
| hideCountryCode     | 是否隐藏区号选择框            | boolean        | false        | 1.0.9  |
| tips     | 帮助文本            | ReactNode        | -        | 1.0.9  |
| countryCode     | 显示区号            | number        | -        | 1.0.9  |
| validate     | 输入限制            | function        | -        | 1.0.9  |
| check     | 检验是否开启            | boolean        | true        | 1.0.9  |
| required     | 是否必填            | boolean        | false        | 1.0.9  |
| onSuccess     | 校验成功回调            | (value, country_code, country) => void         | -        | 1.0.9  |
| onError     | 校验失败回调            | (value, country_code, country, id) => void         | -        | 1.0.9  |
| value     | 初始输入框值            | string         | -        | 1.0.9  |
| editable     | 设置为 false 时，区域选择无法打开            | boolean         | true        | -  |
| browser     | 是否开启浏览态            | boolean         | false        | -  |
| browserStyle     | 浏览态样式            |    CSSProperties      | -        | -  |
| browserClassName     | 浏览态类名            | string         | -        | -  |
| customRender     | 浏览态显示内容，设置此值后，将不解析任何传入的值，只显示此函数返回值            | fun         | -        | -  |
| displayFormat     | 失焦后的位数格式配置，浏览态同样适用，优先级低于customRender            | string         | -        | -  |

### 类型说明

```js
interface countryListType {
  country: string;
  country_code: number;
  // 可选属性
  [key: string]: any; // 允许其他任意属性
}
```

### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | `${fieldid}_mobile` | 1.0.9  |
| 下拉框 | `${fieldid}_mobile_select` | 1.0.9  |
| 输入框 | `${fieldid}_mobile_input` | 1.0.9  |