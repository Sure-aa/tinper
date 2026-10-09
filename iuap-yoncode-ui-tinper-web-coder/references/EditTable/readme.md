---
tags:
  - TinperNextPro
  - EditTable组件
---
# EditTable 编辑表格

<!--EditTable-->
## API

- 默认继承[Table](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-table/other)
- 特有属性如下：
### Table props

| 参数                    | 说明                                     | 类型                                    | 默认值             | 版本  |
| :--------------------- | :--------------------------------------- | :------------------------------------- | :-------------- | :------------ |
| type   | 编辑表格类型，目前支持两种（inline：行内单元格编辑;inlineForm行内展开表单编辑）   | inline/inlineForm                    | inline              | 1.0 |
| formProps   | 类型为行内表单时，设置表单属性。可参照dataForm属性   |                   |               | 1.0 |
| autoEditedByClickRows   | 是否支持开启点击行进入编辑状态   | false / 'click' / 'hover'                              | false              | 1.0 |
| rowKey   |  同表格rowKey(`注意：编辑表格下只支持 string 格式`)  | string                              |               | 1.0 |
| isBigData   | 是否开启大数据表格模式   | boolean                              | false              | 1.0 |
| fillSpace | 继承自表格（表格自动填满父级剩余空间） | boolean | true |否| 1.0 |
| isSingleFind   | 是否开启单列查询   | boolean                              | false              | 1.0 |
| isSum   | 是否开启合计行功能   | boolean                              | false              | 1.0 |
| isDragColumn   | 是否开启支持列拖拽   | boolean                              | true              | 1.0 |
| isFilterColumn   | 是否开启列锁定过滤   | boolean                              | true              | 1.0 |
| isSort   | 是否开启支持排序功能   | boolean                              | false              | 1.0 |
| isSingleFilter   | 是否开启单列过滤   | boolean                              | false              | 1.0 |
| saveText   | 保存按钮文本   | string                              | 保存              | 1.0 |   | boolean                              | false              | 1.0 |
| editText   | 编辑按钮文本   | string                              | 编辑              | 1.0 |
| cancelText   | 取消编辑按钮文本   | string                              | 取消              | 1.0 |
| operationItems   | 操作列按钮配置. 参数4-innerOperations：内置编辑，以及编辑态取消，保存按钮。    | operationItemsOptions[] / function(record, index, isEdit, innerOperations) => operationItemsOptions[] | -           | 1.0  |
| operationClick   | 操作按钮点击事件       | function(record,item,e)=>{} 参数：（当前行数据，点击按钮信息，event) | -           | 1.0  |
| operationType    | 操作列类型  'button'/'link'/function(operationItems,record)=>{ReactNode}参数1：处理后的操作配置参数2：当前行数据                       | string /function                  | 'button'        | 1.0  |
| operationTypeProps  | 操作列的其他配置 {maxCount:3,//配置操作列最多显示数量，超出在更多的下拉中进行显示}                 | object                  |    {maxCount:3}      | 1.0  |


### Column props

| 参数                    | 说明                                     | 类型                                    | 默认值             | 版本 |
| :--------------------- | :--------------------------------------- | :------------------------------------- | :-------------- | :-------|
| editType   | 编辑类型(`'input' /'textarea'/ 'select' / 'date' / 'time' / 'switch' /'treeselect'/ 'number' / 'inputNumberGroup'/'rangepicker' / 'cascader' / 'radiogroup' / 'checkboxgroup/'custom'`)    | string                             |  editAbled=true,没有配置renderFormItem，默认为input            | 1.0 |
| editOptions   | 单元格可编辑组件属性配置集合（函数主要是为了解决行数据联动效果）   | Object/function(record,  index,  { isEdit, isAdd, editAbled })=>Object                           | -              | 1.0 |
| editAbled   |  该列是否可编辑，具有组件编辑决定权  | boolean / Functio(record, index, column)                             |         true      | 1.0 |
| onCellChange   | 单元格值改变后的回调   | Function(record, column, value)                            | -              | 1.0 |
| render   |  单元格显示内容。继承自table render，参数结构扩展了第四个参数  | (text,record, index,{ isEdit, isAdd, editAbled, column })=>React.ReactNode                              |         -      | 1.0|
| renderFormItem   |  自定义编辑态的编辑结构(要求自定义表单组件必须支持value和onChange,否则无法拿到正确的值),封装方法和使用方式和Form.Item自定义组件一致  | (form,record, index,column)=>React.ReactNode                              |         -      | 1.0|
| textToFormItemValue   |  当数据库该列数据和可编辑单元格值格式不一致，可用该方法进行转换  | textToFormItemValue(text, record, col, index)=>formitemValue:any                             |         -      | 1.0|
| editTip   |  编辑时的辅助提示信息  | string                              |         -      | 1.0|
| validator   |  自定义单元格校验规则  | (value: any, record: any, data: any, callback: any) =>void                              |         -      | 1.0|
| patternMsg   |  正则验证失败时给出的错误提示消息  | string                              |         -      | 1.0|
| helpTip   |  非编辑时的辅助提示信息  | string                              |         -      | 1.0|
| editTip   |  编辑时的辅助提示信息  | string                              |         -      | 1.0|
| showEllipsisTitle   |  title内容在阅读状态是否显示  | boolean                              |         true      | 1.0|


`特别强调:`
-  列的renderFormItem只负责自定义渲染编辑态单元格；单元格onChange输出的值，对应的是属性data该列字段的值，如果想在单元格回显正确，需要遵循表单项value的值结构。`原理和formItem的使用规则一致`。
- 列的render方法，只负责渲染只读单元格的时候的内容。编辑单元格拿回来的数据，通过参数`（text,record, index,{ isEdit, isAdd, editAbled, column }）`text字段获取，第四个参数，包含当前列的配置信息，可将值反射成label内容。
    - 比如demo中的`曾住地址`列：
```js
    // 1. 列配置
const columns = [
    {
    title: "曾住地址",
    dataIndex: "oldAdds",
    key: "oldAdds",
    width: 200,
    children: [],
    editType: 'checkboxgroup',
    render: (text, record, index, { column }) => {
        const options = column.editOptions.options;
        return text
        ? text.map(item => {
            return options.filter(option => option.value === item)[0].label;
        }).join()
        : "-"
    },
    editOptions: {
        options: [
        { label: '北京', value: 'bj' },
        { label: '天津', value: 'tj' },
        { label: '成都', value: 'cd' }
        ]
    }
    }
]
// 2. editOptions.options是Select(@tinper/next-ui)组件下拉选项， 选项最终的值”value“字段，那么数据提交给data的是`bj|tj|cd`
// 3. 那么想要回显在单元格的只读内容，则需要在render方法将value，通过editOptions.options转换成label.

```


### operationItemsOptions
| 参数                    | 说明                                     | 类型                                    | 默认值             | 版本  |
| :--------------------- | :--------------------------------------- | :------------------------------------- | :-------------- | :------------ |
| key   | 按钮的key   | string                              | -              | 1.0 |
| text   |  按钮显示名称  | string                              |      -         | 1.0 |
| otherProps   | button的其他配置   | object                              | {}              | 1.0 |

## 方法说明

- 特有方法如下：
  
```js
/**
 * 在第一行新增数据
 * @param rowData 插入的数据[无rowData，则组件内部内置一条数据]
 * @param callback 更新后的回调
 */
addRow: (options: {rowData: Object[], callback: Function}) => {}
```
```js
/**
 * 在最后一行新增数据
 * @param rowData 插入的数据[无rowData，则组件内部内置一条数据]
 * @param callback 更新后的回调
 */
addRowLast: (options: {rowData: Object[], callback: Function}) => {}
```
```js
/**
 * 在某一行子级插入数据
 * @param rowData 插入的数据[无rowData，则组件内部内置一条数据]
 * @param callback 更新后的回调
 */
addRowChild: (options: {rowKey: string; rowData: Object[], callback: Function}) => {}
```
```js
/**
 * 某一条数据前插入
 * @param rowKey 行rowKey
 * @param rowData 插入的数据[无rowData，则组件内部内置一条数据]
 * @param callback 更新后的回调
 */
addRowBefore: (options: { rowKey: string; rowData: Object[]; callback: Function }) => {}
```
```js
/**
 * 某一条数据后插入
 * @param rowKey 行rowKey
 * @param rowData 插入的数据[无rowData，则组件内部内置一条数据]
 * @param callback 更新后的回调
 */
addRowAfter: (options: { rowKey: string; rowData: Object[]; callback: Function })=>{}
```
```js
/**
 * 获取正在编辑的行的rowKey
 */ 
getIsEditKey: () => {}
```
```js
/**
 * 清除所有行的编辑状态
 * @param callback 更新后的回调
 */
clearEditAll: (options: {callback: Function}) => {}
```
```js
/**
 * 清除所有数据
 * @param callback 更新后的回调
 */
clearAllData: (options: {callback: Function}) => {}
```
```js
/**
 * 将指定行设置为编辑态或者非编辑态
 * @param rowKey 行rowKey
 * @param edit true: 编辑态，false：非编辑态
 * @param callback 更新后的回调
 */
editRow: (options: {rowKey: string, edit: boolean, callback: Function}) => {}
```
```js
/**
 * 更新整个行数据 (upDate)
 * @param rowData 要更新的行数据
 * @param callback 更新后的回调
 */
saveRowData: (options: {rowData: Object, callback: Function} ) => {}
```
```js
/**
 * 取消保存
 * @param rowKey 行rowKey
 */
cancel: (options: {rowKey: Key} ) => {}
```
```js
/**
 * 删除指定行(支持单个删除和多个删除)
 * @param rowKey string | string[]
 * @param callback 更新后的回调
 */
deleteData: (options: {rowKey: string | string[], callback: Function}) => {}
```
```js
/**
 * 获取全部数据
 */ 
getAllData: () => {}
```
```js
/**
 * 获取新增数据的keys
 */ 
getAddRowKeys: () => {}
```
```js
/**
 * 获取新增的数据
 */ 
getAddRows: () => {}
```
```js
/**
 * 获取当前选中行的keys
 */ 
getSelectedRowKeys: () => {}
```
```js
/**
 * 设置选中行的key
 * @param rowKey string | string[]
 */
setSelectedRowKeys: (options: {rowKey: string | string[]}) => {}
```
```js
/**
 * 获取当前选中行的数据
 */ 
getSelectedRows: () => {}
```
```js
/**
 * 清空全选
 */ 
clearSelectedRowKeys: () => {}
```
```js
/**
 * 获取已编辑过的行Keys
 */ 
getEditRowKeys: () => {}
```
```js
/**
 * 获取已编辑过的数据
 */ 
getEditRows: () => {}
```
```js
/**
 * 获取已删除行Keys
 */ 
getDeleteRowKeys: () => {}
```
```js
/**
 * 获取已删除的数据
 */ 
getDeleteRows: () => {}
```
```js
/**
 * 通过行键值获取指定行数据
 * @param rowKey string | string[]
 */
getRowDataByKey: (options: {rowKey: string | string[]}) => {}
```
```js
/**
 * @description: 获取指定单元格数据
 * @param {*} rowKey : 单元格行对应的键
 * @param {*} dataIndex：单元格对应列的dataIndex
 */
getCellDataByKey: (options: {rowKey: string, dataIndex: string}) => {}
```
```js
/**
 * 更新指定列下的单元格值
 * @param dataIndex 列数据索引名
 * @param cellValue 单元格更新后的值
 * @param callback 更新后的回调
 */
saveColumnData: (options: {dataIndex: string, cellValue: string, callback: Function}) => {},
```
```js
/**
 * 从指定行开始向上更新指定列下的单元格值
 * @param rowKey 当更新方式为 up|down 时，必须指定此参数值
 * @param dataIndex 列数据索引名
 * @param cellValue 单元格更新后的值
 * @param upNum 向上填充的行数
 * @param callback 更新后的回调 参数是（newData, cellErrors）
 */
saveColumnDataFillUp: (options: {rowKey: string, dataIndex: string, cellValue: string, fillNum: number, callback: Function}) => {}
```
```js
/**
 * 从指定行开始向下更新指定列下的单元格值
 * @param rowKey 当更新方式为 up|down 时，必须指定此参数值s
 * @param dataIndex 列数据索引名
 * @param cellValue 单元格更新后的值
 * @param fillNum 向下填充的行数
 * @param callback 更新后的回调 参数是（newData, cellErrors）
 */
saveColumnDataFillDown: (options: {rowKey: string, dataIndex: string, cellValue: string, fillNum: number, callback: Function}) => {}
```
```js
/**
 * 更新指定行键值对应的多个单元格的数据（即：更行数据）
 * @param rowData 行数据
 * @param callback 更新后的回调 参数是（newData, cellErrors）
 */
saveMultiCellData: (options: {rowData: Object, callback: Function}) => {}
```
```js
/**
 *获取所有单元格的错误消息
* 格式如下：
*  {
*     '行键值1':{
*          'A字段键值':'A错误描述',
*          'B字段键值':'B错误描述',
*          ...
*     },
*     '行键值2':{
*          'A字段键值':'A错误描述',
*          'B字段键值':'B错误描述',
*          ...
*     },
*     ...
*  }
*/
getAllCellError: () => {}
```
```js
/**
 * 设置所有单元格的错误消息，cellErrors错误消息对象集合格式必须是通过addCellError方法构建的错误消息内容格式。
 * 内容格式参看getAllCellError()方法返回的格式。
 */
setAllCellError: (options:{ cellErrors: json, callback: Function}) => {}
```
```js
/**
*  给cellErrors对象集合里面添加或者更新一个新的单元格错误消息。
*  options={
*    @param rowKey 当更新方式为 up|down 时，必须指定此参数值s
*    @param dataIndex 列数据索引名
*    @param errorMsg string 描述错误
*  }
* @return 添加后的错误消息集合对象，内容格式参看getAllCellError()方法返回的格式。
*/
updateCellError: (options: {rowKey: string, dataIndex: string, errorMsg: string}) => {}
```
```js
/**
* 清除指定单元格的错误消息
* options={
*   @param rowKey string 行键值
*   @param dataIndex string 列定义键值
* }
*/
clearCellError: (options: {rowKey: string, dataIndex: string}) => {}
```
```js
/**
* 获取指定单元格的错误消息
* options={
*  @param rowKey string 行键值
*  @param dataIndex string 列定义键值
* }
*/
getCellError: (options: {rowKey: string, dataIndex: string}) => {}
```
```js
/**
 * 将指定行进行移动
 * 参数options列表
 * @param rowKey string|array 需要移动的行键值，一般为勾选的行键值
 * @param clearSelected 移动完是否清除选中
 * @param pos number 移动的位置 负数表示上移，正数表示下移，例如：-1 为上移一行、1 为下移一行
 * @param callback 移动完成后的回调
 */
rowMoveTo: (options: {rowKey: string | string[], pos: number, callback: Function}) => {}
```
```js
/**
 * 表格验证
 * @param range 'all' | 'row' | 'cell'  默认all,验证表格范围
 * @param callback Function 验证的回调函数，参数为所有的验证信息
 */
validate: (options: {callback : Function}) => {}
```

### fieldid 场景说明：

| 场景          | 生成规则说明  |  版本 |
| ---------------- | ---- |---- |
| 根元素 | fieldid | 1.0  |
| 行操作按钮 | `${fieldid}_operations_item_${item.key}` | 1.0  |
| 行操作-下拉按钮 | `${fieldid}_operations_dropdownbtn` |  1.0  |
| 行操作-下拉菜单 | `${fieldid}_operations_dropdown_menu` |  1.0  |
| 行操作-超出最大数量按钮 | `${fieldid}_operations_maxcountbtn` |  1.0  |
