---
tags:
  - TinperNextPro
  - TableTransfer组件
---
# TableTransfer 列表穿梭

<!--TableTransfer-->
## API

- 列表穿梭参照组件
### 属性api
| 参数                    | 说明                                     | 类型                                    | 默认值             | 版本  |
| :--------------------- | :--------------------------------------- | :------------------------------------- | :-------------- | :------------ |
|searchPlaceholder|搜索区placeholder(作用域已选和待选区域)|String|-|1.0.6|
|leftColumns|左侧待选区列配置 |Array(具体配置和Table一致)|-|1.0.6|
|rightColumns|已选区列配置 |Array(具体配置和Table一致)|-|1.0.6|
|titles|标题配置 |Array<string>|-|15.3.0|
| rowKey   |  同表格rowKey(`注意：编辑表格下只支持 string 格式`)  |string       |   "id" | 1.0.6 |
|data|待选区数据源数据|Array|-| 1.0.6 |
|searchContent|参照查询区扩展|ReactDom /Function=>ReactNode|-| 1.0.6 |
|showSearch|是否显示左侧待选区表格右肩搜索按钮|boolean|true| 1.0.6 |
|searchWrapper|扩展tab处搜索框|function(searchNode, {searchWord})|-| 1.0.8 |
|onSearchChange|左侧待选区简单搜索文本变化触发函数|Function（searchWrod）=>void |-| 1.0.6 |
|onSearch|左侧待选区简单搜索enter或者点击搜索按钮触发事件|Function（searchWrod）=>void |-| 1.0.6 |
|filterOption|数据条目过滤函数，左侧待选区前端过滤时，可配置，如果同时配置onSearchChange或者onSearch时，不生效；已选区则前端过滤|Function（searchWrod, item, direction）=>boolean |-| 1.0.6 |
|showSelectAll|左侧待选区表格右肩选择全部按钮是否显示|boolean |true| 1.0.6 |
|onSelectAll|左侧待选区表格右肩选择全部按钮事件|Function（）=>void |-| 1.0.6 |
|onClearSelectAll|已选区清空选择全部按钮事件|Function（）=>void |-| 1.0.6 |
|onSelectChange|待选区选项变化事件|Function（seletedRowkeys, selectedRowData）=>void |-| 1.0.6 |
|targetData|已选区被选中的数据,当左侧表格数据后端分页，作为手控组件显示数据用|Array |-| 1.0.6 |
|pagination|待选区分页配置，配置和DataTable一致,参照默认为简单分页|boolean/Object |-| 1.0.6 |
|disabled|是否禁用参照|boolean|false| 1.0.6 |


### 方法说明

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