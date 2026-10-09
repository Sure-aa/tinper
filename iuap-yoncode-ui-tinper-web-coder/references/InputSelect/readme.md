---
tags:
  - TinperNextPro
  - InputSelect组件
---
# InputSelect 下拉搜索

<!--InputSelect-->
## API

- 属性如下：

| 参数             | 说明                                           | 类型                      | 默认值      | 版本 |
| ---------------- | ---------------------------------------------- | ------------------------- | ----------- | ---- |
| placeholder     | input框提示信息               | string               | -          | 1.0  |
| value     | input框值 |  string               | -          | 1.0  |
| rowKey     | 匹配表格数据的字段               | string               | -          | 1.0  |
| labelKey     | 匹配表格数据的字段，优先级大于rowKey               | string               | -          | 1.0  |
| columns     | 表格列的配置表               | array               | - | 1.0  |
| dataSource | 表格数据 | array               | - | 1.0  |
| showHeader | 是否显示表头 | boolean | true | 1.0  |
| multiple | 是否多选 | boolean | false | 1.0  |
| onChange | 选择表格数据时的回调 | function(value)               | - | 1.0  |
| disabled | 是否禁用 | boolean | false | 1.0  |
| tableWidth | 下拉层宽度 | Number | 400 | 去除，默认与输入框同宽  |
| className | 自定义类名 | string | - | 1.0  |
| popoverClassName | 自定义弹层类名 | string | - | 1.0  |
| allowClear | 是否支持清除 | boolean | true | 1.0  |
| maxTagCount | 最多显示多少个 tag | number | - | 1.0  |
| maxTagTextLength | 最大显示的 tag 文本长度 | number | 1 | 1.0  |
| onSearch | 输入框搜索回调 | function | 1 | 1.0  |
<!-- | filterKey | 最大显示的 tag 文本长度 | number | 1 | 1.0  | -->
