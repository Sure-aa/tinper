---
tags:
  - TinperNextPro
  - GroupCascader组件
---
# GroupCascader 级联分组

<!--GroupCascader-->
## API


| 参数 | 说明 | 类型 | 默认值 | 版本 |
| --- | --- | --- | --- | --- |
| options                | 下拉列表数据，（注：和基础级联组件比较，每项数据中添加（groupTopKey、groupContentKey、isGroupNum）属性，groupTopKey表示，在同级数据中当前数据属于哪项分组，groupContentKey表示在groupTopKey大分组下，此项数据属于groupTopKey分组下的小分组（面板数据左侧分组，像通讯录侧边的字母分组），isGroupNum表示当前层级是否需要分组的规则数（为0表示当前层级需要分组，不是0的数据，大于此数据分组，小于此数据不分组）），[{lable:'xxx',value:'yyy',groupTopKey:'abcd',groupContentKey:'b',isGroupNum: 15},....]   | json            | 无默认值，必填       | - |
| loadDataFlag           | 是否使用懒加载标识 | boolean            | false | - |
| searchValue            | 懒加载搜索之后获取的到数据，回填给组件的数据，数据格式为：[{name: '基础组件/导航/标签', value: ['jczj', 'dh', 'bq'], path: [{label: '基础组件', value: 'jczj', children: [{label: '导航', value: 'dh', children: [{label: '标签', value: 'bq'}]}]}, {label: '导航', value: 'dh',  children: [{label: '标签', value: 'bq'}]}, {label: '标签', value: 'bq'}]}, ...], 具体配置见下表。注：当loadDataFlag为true时生效  | Array | -       | - |
|placeholder    |input提示信息|    string    |""| - |
|allowClear    |是否支持清除|    boolean    |true| - |
|bordered|设置边框，支持无边框、下划线模式|`boolean`、`bottom`| -|-|
|align|设置文本对齐方式|`left`、`center`、`right`|  -|-|
|autoFocus    |自动获取焦点|    boolean    |false| - |
|className    |自定义wui-cascader-picker层类名|    string    |-| - |
|getPopupContainer    |菜单渲染父节点| `HTMLElement` `() => HTMLElement`  `Selectors` |`body`| - |
|loadData    |用于动态加载选项，无法与 showSearch 一起使用|    (selectedOptions) => void    |-| - |
|showSearch    |在选择框中显示搜索框|    boolean    |false| - |
|notFoundContent    |当下拉列表为空时显示的内容|    string    |-| - |
|suffixIcon    |自定义选择框后缀图标|    ReactNode    |-| - |
|defaultValue|默认的选中项格式为：[{lable:'xxx',value:'yyy'},....] 或者 ['key1','key3','key3',...]|    string[] | []| - |
|value|受控的值格式为：[{lable:'xxx',value:'yyy'},....] 或者 ['key1','key3','key3',...]|    string[] | [] | - |
|disabled|禁用|    boolean|false| - |
|size|输入框大小，可选 lg md sm|    string|'md'| - |
|onChange   |选择完成后的回调| Function(value, selectedOptions)|    -| - |
|separator    |分隔符自定义| string |'/ '| - |
|onSearch   |监听搜索，返回输入的值和匹配的值| Function(value, selectedOptions)|    -| - |
|locale | 语言 | string | zh-cn | - |
|popupVisible | 是否显示浮层 | boolean | false | - |
|onPopupVisibleChange | 显示/隐藏浮层的回调 | (value) => void | - | - |

### searchValue
| 参数 | 说明 | 类型 | 默认值 | 版本 |
| --- | --- | --- | --- | --- |
| name            | 懒加载搜索时, 面板展示的内容项   | string  | -      | - |
| value           | 懒加载搜索项，对应的值 | array            | - | - |
| path            | 懒加载搜索项，对应的全路径的值，这里需给出全路径（除了叶子节点外，每项都应存在children），因搜索出来的值不是根据options内的数据获取的，为了保证value值能正常显示  | array    | - | - |