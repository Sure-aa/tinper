---
tags:
  - TinperNextPro
  - Identity组件
---
# Identity 证件号

<!--Identity-->
## API

- 属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| placeholder     | 提示信息               | string               | -          | 1.0.9  |
| value | 证件号当前值。idType代表下拉前缀，“1”-“4”分别表示“身份证”“军官证”“护照”“银行卡”；identity表示输入框中的值 | { idType: string, identity: string } | { idType: "1", identity: "" }  | 1.0.9  |
| disabled     | 是否禁用               | boolean               | false         | 1.0.9  |
| readOnly     | 是否只读               | boolean               | false         | -  |
| idTypes     | 证件号可选类型               | 参照idTypesInit               | idTypesInit         | 1.0.9  |
| bordered     | 设置边框，支持无边框、下划线模式               | boolean/bottom               | true         | 1.0.9  |
| formatter     | 证件号类型格式化             | string             | -         | 1.0.9  |
| onChange     | 内容变化回调              | ({idType, identity, isSelectChange}) => void             | -         | 1.0.9  |
| onIdentityChange     | 下拉框变化回调    | ({idType, identity}) => void             | -         | -  |
| onBlur     | 失焦回调              | ({idType, identity}) => void             | -         | 1.0.9  |
| onFocus     | 输入框聚焦回调              | ({idType, identity}) => void             | -         | 1.0.9  |
| className     | 自定义类名              | string             | -         | 1.0.9  |
| allowClear     | 是否显示清空按钮               | boolean               | true      | 1.0.9  |
| style     | 自定义样式              | React.CSSProperties             | -         | 1.0.9  |
| showSelect     | 是否显示证件号类型下拉选项              | boolean             | true         | 1.0.9  |
| check     | 是否开启校验               | boolean               | false      | 1.0.9  |
| pattern     | 检验正则               | RegExp               | -      | 1.0.9  |
| required     | 是否必填               | boolean               | false      | 1.0.9  |
| customCheck     | 自定义校验规则，返回 true 检验成果，false 校验失败               | (val: string) => boolean               | -      | 1.0.9  |
| onError     | 校验失败回调               | (val: string, pattern: RegExp) => void             | -      | 1.0.9  |
| onSuccess     | 检验成功回调               | (val: string) => void             | -      | 1.0.9  |
| locale     | 语言               | string         | zh-cn      | 1.0.9  |
| inputProps     | 输入框属性               | {}         | -      | -  |
| selectProps     | 下拉框属性               | {}         | -      | -  |
| browser     | 是否开启浏览态               | boolean        | false     | -  |
| browserStyle     | 浏览态样式              | CSSProperties        | -     | -  |
| browserClassName     | 浏览态类名              | string        | -     | -  |
| selectOptionStyle    | 下拉选项的单条样式设置    | React.CSSProperties        | -     | -  |

### 类型说明

```js
idTypesInit = {
    1: { name: '身份证', formatter: '### ### #### #### ####' },
    2: { name: '军官证', formatter: '##################' },
    3: { name: '护照', formatter: '#### ####' },
    4: { name: '银行卡', formatter: '#### #### #### ####' }
  };
```

### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | `${fieldid}_identity` | 1.0.9  |
| 下拉框 | `${fieldid}_identity_select` | 1.0.9  |
| 输入框 | `${fieldid}_identity_input` | 1.0.9  |