---
tags:
  - TinperNextPro
  - DataTable组件
---

# DataTable 数据表格

<!--DataTable-->
## API

- 默认继承[Table](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-table/bip)

以下为特有属性：

### 显示或者布局类属性

|参数|业务含义 |类型|默认值|是否必填|版本 |
|--|--|--|--|--|--|
| mode | 表格展示形式 | string `[card \| table]` | table |否| 1.0 |
| showModeSwitch | 是否默认展示表格和卡片表格切换按钮组 | boolean | true | 否| 1.0 |
| showSelectionFilter | 是否开启已选过滤 | boolean | true | 否| 1.0 |
| onChangeSelectionFilter | 已选过滤开关切换事件 | (checked:boolean, rowKeys:any[], rowData:any[])=>void | - | 否| 1.0 |
| showRowNum | 序号列，数据表格内部内置序号列计算逻辑，从(current - 1)*pageSize +1开始作为当前页的起始序号| boolean|object(结构和基础表格一致) | false | 否| 1.0 |
| renderToolBar | 表格 toolbar 自定义渲染 | function():ReactNode | - |否| 1.0 |
| toolBarClassName | 自定义 toolbar 类名 | string | - | 否|1.0 |
| searchContent | 自定义搜索区域 | React.ReactNode | - |否| 1.0 |
| fillSpace | 继承自表格（表格自动填满父级剩余空间）如果scroll.y配置的时候，以scroll为优先 | boolean | true |否| 1.0 |
| itemType | 卡片表格独有属性，卡片布局方式。 | "horizontal" | "vertical" | ((record:iDataItem, index:number)=>React.ReactNode) | |否| 1.0 |
| columnCount | 卡片表格独有属性。每行显示多少个卡片。 | number | Object({ xs: 8, sm: 16, md: 24}) | |否| 1.0 |
| gutter | 卡片表格独有属性。卡片之间间隙。 | number | object({ xs: 8, sm: 16, md: 24}) | array | [16,16] |否| 1.0 |
| rowActiveKeys | 行是否处于点击状态 | Array/boolean | - |否| 1.0.9 |

### 和高阶函数相关属性

|参数|业务含义 |类型|默认值|是否必填|版本 |
|--|--|--|--|--|--|
| isSingleFind | 是否开启单列查找定位功能 | boolean | true |否| 1.0 |
| isSum | 是否开启合计功能 | boolean | false |否| 1.0 |
| isDragColumn | 是否开启拖拽列功能 | boolean | true |否| 1.0 |
| isFilterColumn | 是否开启列过滤功能 | boolean | true |否| 1.0 |
| isSort | 是否开启列排序功能 | boolean | false |否| 1.0 |
| sort | 排序功能配置{ mode:'single'//单列排序, backSource:false //如果是前端排序为false，后端排序为true } | object | {} |否| 1.0 |
| isSingleFilter | 是否开启单列过滤功能 | boolean | false |否| 1.0 |
| isBigData | 是否开启大数据渲染 | boolean | false |否| 1.0 |

### 数据请求相关属性
|参数|业务含义 |类型|默认值|是否必填|版本 |
|--|--|--|--|--|--|
| pagination | 分页信息 {current:1,pageSize:20,onChange:()=>{},pageSizeOptions: ["10", "20", "30", "50", "80", "100", "200", "500", "1000"],showSizeChanger:true,其他继承基础组件 Pagination 的属性配置，可覆盖}。配置request请求时，默认开启分页;否则默认关闭分页。 | boolean/object|-- | 否 | 1.0 |
| autoQuery | 自定义请求是否在首次渲染自动触发 | boolean | true |否| 1.0 | 
| params | 自定义携带的额外参数 | any | - |否| 1.0 | 
| request | 自定义请求 | function(params:{page:{current,pageSize},sort:[],params:any})=>{return Promise<{success:boolean,data:[],total?:number}>} 如果配置请求，但是不返回total会认为是请求一次，数据进行前端分页 | - |否| 1.0 | 
| postData|请求返回的数据处理，处理后的结果会作为表格data,以及作为onRequestSuccess的参数传出去|function(dataSource)=>newDataSource|-|否|1.0|
| onRequestSuccess |请求成功钩子，每次请求都会触发，比如翻页，过滤，排序|function(dataSource:[])=>void|-|否|1.0|
| onRequestError |请求失败对外暴露的钩子|function(e)=>void|-|否|1.0|

### 表格操作配置相关属性

|参数|业务含义 |类型|默认值|是否必填|版本 |
|--|--|--|--|--|--|
| operationItems | 操作列按钮配置 | [object]/function(record)=>{return newOperationItems}参数 1：处理后的操作配置参数 2：当前行数据 ; `object:{key:'',text:'buttonName'//按钮名称,render:function(record, index, childDom, operationItemConfig)=>ReactDom//如果只是做自定义外层容器内容，可用第三个参数；如果完全自定义dom，第四个参数返回所有当前操作按钮的配置信息，**注意：会包含isMenuItem字段判断当前是否在下拉选项中还是展开的行操作按钮中，需自己判断做自定义dom**,otherProps:{disabled:boolean,...}//button 的其他配置, hidden:boolean/Function(record)=>boolean 是否隐藏，rowActivable:true(是否触发操作行高亮),onClick:function(record, index)}` ;返回新的 operationItems 或者完整的操作列 | - |否| 1.0 |
| operationClick | 操作按钮点击事件 | function(record,item,e, index)=>{} 参数：（当前行数据，点击按钮信息，event） | - |否| 1.0 |
| operationType | 操作列类型 'button'/'link'/function(operationItems,record)=>{return newOperationItems / ReactNode}参数 1：处理后的操作配置参数 2：当前行数据 ; 返回新的 operationItems 或者完整的操作列 | string /function | 'button' |否| 1.0 |
| operationTypeProps | 操作列的其他配置 {maxCount:3,//配置操作列最多显示数量，超出在更多的下拉中进行显示,rowActiveKeysMode:true// 行点击高亮背景模式（数据表格独有属性；(single/multiple)/boolean）,hoverVisible:false,//是否卡片 hover 时才显示操作按钮} | object | {maxCount:3,hoverVisible:false, rowActiveKeysMode:true } |否| 1.0 |
| rowSelection | 行选中相关配置，配置了默认为 checkbox，{} | object | | 否|1.0 |



- 表格数据来源：
1. data传入(和基础表格使用方式一致)；
2. 配置请求信息。


### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | fieldid | 1.0  |
| 行操作按钮 | `${fieldid}_operations_item_${item.key}` | 1.0  |
| 行操作-下拉按钮 | `${fieldid}_operations_dropdownbtn` |  1.0  |
| 行操作-下拉菜单 | `${fieldid}_operations_dropdown_menu` |  1.0  |
| 行操作-超出最大数量按钮 | `${fieldid}_operations_maxcountbtn` |  1.0  |

## DataTable 方法


```js
 // 方法名、参数、返回值、[请求格式,响应格式]
 /**
   * 获取被选中行数据keys
   * 例如：this.tableRef.current.getSelectedRowKeys()
   */
    getSelectedRowKeys:function(){return []}
/**
   * 获取被选中行数据数据
   * 例如：this.tableRef.current.getSelectedRowData()
   */
    getSelectedRowData:function(){return []}
 /**
   * 设置选中项
   * @param selectedRowKeys string[] 选中项keys
   * 例如：this.tableRef.current.setSelectedRowKeys(['1','2'])
   */
    setSelectedRowKeys:function(selectedRowKeys:array){}

/**
   * 获取当前表格数据
   * @return []
   * 例如：this.tableRef.current.getDataSource()
   */
    getDataSource:function(){return []}

/**
   * 获取当前查询条件
   * @return {
   * page: {
   *  current: number,
   *  pageSize: number
   * },
   * sort: [{
   *   order?: string | boolean | null;
   *    orderNum?: number;
   *    field:string
   * }],
   * params:any
   * }
   * 例如：this.tableRef.current.getQueryFilters()
   */
    getQueryFilters:function(){return {}}

/**
   * 清除选中项
   * 例如：this.tableRef.current.clearSelectedRowKeys()
   */
    clearSelectedRowKeys:function(){}

/**
   * 查询数据
   * 参数options列表
   * @param queryOptions  {} 请求参数和getQueryFilters返回的结构一致
   * 例如：this.tableRef.current.queryData({
   *   page: {
   *    current: pageInfo.current,
   *        pageSize: pageInfo.pageSize
    *   },
    *   sort: [{
    *             order?: string | boolean | null;
    *             orderNum?: number;
    *             field:string
    *         }],
    *         params:any
   * })
   */
    queryData:function(queryOptions){}

    /*
    * 清空被选中高亮行keys
    */
    clearRowActiveKeys:function(){}



```