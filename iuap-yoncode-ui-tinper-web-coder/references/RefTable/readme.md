---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

<!--RefTable-->
## API

- 列表穿梭参照组件

### 属性api
| 参数                    | 说明                                     | 类型                                    | 默认值             | 版本  |
| :--------------------- | :--------------------------------------- | :------------------------------------- | :-------------- | :------------ |
|type|列表参照类型，支持单选和多选，radio/checkbox|String|radio|1.0.6|
|title|参照弹窗title|String/ReactNode|-|1.0.6|
|renderFooter|参照footer自定义|Function(FooterButtonGroup)=>ReactNode|-|1.0.6|
|columns|表格列配置 |Array(具体配置和Table一致)|-|1.0.6|
| rowKey   |  同表格rowKey(`注意：编辑表格下只支持 string 格式`)  |string       |   "id" | 1.0.6 |
|data|待选区数据源数据|Array|-| 1.0.6 |
|searchContent|参照查询区扩展|ReactDom /Function=>ReactNode|-| 1.0.6 |
|showSearch|是否显示左侧待选区表格右肩搜索按钮|boolean|true| 1.0.6 |
|onSearchChange|左侧待选区简单搜索文本变化触发函数|Function（searchWrod）=>void |-| 1.0.6 |
|onSearch|左侧待选区简单搜索enter或者点击搜索按钮触发事件|Function（searchWrod）=>void |-| 1.0.6 |
|filterOption|数据条目过滤函数，左侧待选区前端过滤时，可配置，如果同时配置onSearchChange或者onSearch时，不生效；已选区则前端过滤|Function（searchWrod, item, direction）=>boolean |-| 1.0.6 |
|onSelectAll|左侧待选区表格右肩选择全部按钮事件|Function（）=>void |-| 1.0.6 |
|onClearSelectAll|已选区清空选择全部按钮事件|Function（）=>void |-| 1.0.6 |
|onSelectChange|待选区选项变化事件|Function（seletedRowkeys, selectedRowData）=>void |-| 1.0.6 |
|targetKeys|已选区被选中的数据keys|Function（）=>void |-| 1.0.6 |
|targetData|已选区被选中的数据,当左侧表格数据后端分页，作为手控组件显示数据用|Array |-| 1.0.6 |
|pagination|分页配置，配置和DataTable一致,参照默认为简单分页|boolean/Object |-| 1.0.6 |
|value|作为表单项使用，可受控value|Array |-| 1.0.6 |
|onChange|数据变化，点击确认时触发的事件|Function(value) |-| 1.0.6 |
|labelInValue|value是否为对象数组返回，格式[{label:string,value:any}]|boolean|true| 1.0.6 |
|fieldNames|参照回显字段映射关系|Object|{label:"name", value:rowKey,}| 1.0.6 |
|allowClear|是否显示参照触发文本框清空按钮|Object|false| 1.0.6 |
|onClear|参照触发文本框清空按钮清除所有选项事件|Function|-| 1.0.6 |
|maxTagCount|数据回显文本框内最多显示的标签数量，多出来的内容以数字展示|"auto"/number|多选时默认“auto”| 1.0.6 |
|placeholder|数据回显文本placeholder|string|-| 1.0.6 |
|disabled|是否禁用参照|boolean|false| 1.0.6 |
|show|参照弹窗是否可见|Boolean|false|1.0.6|
|onOk|参照弹窗确认|Function（keys, data）|-|1.0.6|
|onCancel|参照弹窗取消事件|Function（keys, data）|-|1.0.6|
|onRowDoubleClick|表格行双击|Function（record, index, event）|-|1.0.6|
|modalProps|弹窗剩余配置项（title，show，onCancelApi除外）|Object|false|1.0.6|
|tableProps|表格剩余配置项（rowKey，data，columns,showSelectionFilter,rowSelection除外）|Object|false|1.0.6|


### 方法说明
```js
/**
 * 打开参照弹窗
 * @param 
 */
openModal: () => {}
```

```js
/**
 * 关闭参照弹窗
 * @param 
 */
closeModal: () => {}
```

```js
/**
 * 清空选项
 * @param 
 */
clearSelect: () => {}
```

```js
/**
 * 获取被选择的数据keys
 * @param 
 */
getTagetKeys: () => {}
```

```js
/**
 * 获取被选择的数据
 * @param 
 */
getTagetData: () => {}
```