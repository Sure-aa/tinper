---
tags:
  - TinperNext
  - provider组件
---
# 全局化配置 ConfigProvider

ConfigProvider 组件，在使用时，需要将你的 App 跟组件包裹起来。这样才能影响到所有使用的子组件。

## API

<!--ConfigProvider-->

| 参数     | 说明                                         | 类型                      | 默认值     | 版本     |
| -------- | -------------------------------------------- | ------------------------- | ---------- | -------- |
| locale   | 设置的语言对象                               | object                    | 中文语言包 | v4.0.0   |
| antd     | 设置和 antd 返回参数一致                     | bool                      | false      | v4.0.0   |
| size     | 设置组件的尺寸                               | string                    | -          | v4.0.0   |
| browser  | 浏览态                                       | bool                      | -          | v15.4.0  |
| disabled | 禁用                                         | bool                      | false      | 4.5.0    |
| readOnly | 只读                                         | bool                      | false      | v15.12.0 |
| layout   | 表单布局                                     | `vertical`\|`horizontal`  | -          | v15.5.1  |
| bordered | 设置输入类组件的边框，支持无边框、下划线模式 | `boolean`\|`bottom`       | -          | v4.5.2   |
| align    | 设置输入类组件的文本对齐方式                 | `left`\|`center`\|`right` | -          | v4.5.2   |
| table    | 设置 Table 组件的通用属性                    | string                    | -          | v4.2.1   |

提供全局设置 locale 方法

```
ConfigProvider.config({locale: 'xxx'})
```
