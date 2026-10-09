---
tags:
  - TinperNext
  - select组件
---
# 下拉框 Select

下拉弹出菜单，代替原生的选择器。支持多选、级联、搜索过滤单选和搜索过滤多选与自动填充选择。

## 组件特性

- 支持单选、多选、标签模式
- 支持搜索过滤
- 支持自定义选项
- 支持键盘操作
- 支持虚拟滚动
- 支持可调整大小


## API

### Select 属性

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|--------|------|
| allowClear | 支持清除 | boolean | false | - |
| autoClearSearchValue | 是否在选中项后清空搜索框，只在 `mode` 为 `multiple` 或 `tags` 时有效 | boolean | true | - |
| autoFocus | 默认获取焦点 | boolean | false | - |
| requiredStyle | 必填样式 | boolean | false | 4.6.6 |
| bordered | 设置边框，支持无边框、下划线模式 | `boolean` \| `bottom` | - | 4.5.2 |
| align | 设置文本对齐方式 | `left` \| `center` \| `right` | - | 4.5.2 |
| clearIcon | 自定义的多选框清空图标 | ReactNode | - | - |
| defaultActiveFirstOption | 是否默认高亮第一个选项 | boolean | true | - |
| defaultOpen | 是否默认展开下拉菜单 | boolean | - | - |
| defaultValue | 指定默认选中的条目 | string \| string[] \| number \| number[] \| LabeledValue \| LabeledValue[] | - | - |
| disabled | 是否禁用 | boolean | false | - |
| readOnly | 是否只读 | boolean | false | 15.5.x |
| browser | 是否设置浏览态 | boolean | false | 15.5.x |
| dropdownClassName | 下拉菜单的 className 属性 | string | - | - |
| dropdownMatchSelectWidth | 下拉菜单和选择器同宽 | boolean \| number | true | - |
| dropdownRender | 自定义下拉框内容 | (originNode: ReactNode) => ReactNode | - | - |
| dropdownStyle | 下拉菜单的 style 属性 | CSSProperties | - | - |
| fieldNames | 自定义节点 label、value、options 的字段 | object 例如{ label: 'label', value: 'data-id', options: 'options' } 注意：options 的id字段被处理赋值为data-id | { label, value, options }  | 4.2.1 |
| filterOption | 是否根据输入项进行筛选 | boolean \| function(inputValue, option) | true | - |
| filterSort | 搜索时对筛选结果项的排序函数 | (optionA: Option, optionB: Option) => number | - | - |
| getPopupContainer | 菜单渲染父节点 | function(triggerNode) | () => document.body | - |
| getSelectAttrs | 自定义生成下拉框属性 | function() | - | - |
| id | 下拉框的 id | string | - | - |
| fieldid | 自动化测试专用属性 | string | - | 4.3.0 |
| labelInValue | 是否把每个选项的 label 包装到 value 中 | boolean | false | - |
| listHeight | 设置弹窗最大滚动高度 | number \| boolean | 320 | - |
| loading | 加载中状态 | boolean | false | - |
| locale | 语言 | string | zh-cn | - |
| maxTagCount | 最多显示多少个 tag | number \| `responsive` \| `auto` | - | - |
| maxTagPlaceholder | 隐藏 tag 时显示的内容 | ReactNode \| function(omittedValues) | - | - |
| maxTagTextLength | 最大显示的 tag 文本长度 | number | - | - |
| menuItemSelectedIcon | 自定义多选时当前选中的条目图标 | ReactNode | - | - |
| mode | 设置 Select 的模式 | `multiple` \| `tags` \| `combobox` | - | - |
| notFoundContent | 当下拉列表为空时显示的内容 | ReactNode | `Not Found` | - |
| open | 是否展开下拉菜单 | boolean | - | - |
| optionFilterProp | 搜索时过滤对应的 `option` 属性 | string | `value` | - |
| optionLabelProp | 回填到选择框的 Option 的属性值 | string | `children` | - |
| options | 数据化配置选项内容 | { label, value }[] | - | - |
| placeholder | 选择框默认文本 | string | - | - |
| placement | 选择框弹出的位置 | `bottomLeft` \| `bottomRight` \| `topLeft` \| `topRight` | bottomLeft | 4.2.1 |
| removeIcon | 自定义的多选框清除图标 | ReactNode | - | - |
| searchValue | 控制搜索文本 | string | - | - |
| showArrow | 是否显示下拉小箭头 | boolean | true | - |
| showSearch | 使单选模式可搜索 | boolean | false | - |
| suffixIcon | 自定义的选择框后缀图标 | ReactNode | - | - |
| tagRender | 自定义 tag 内容 render | (props) => ReactNode | - | - |
| tokenSeparators | 在 `tags` 和 `multiple` 模式下自动分词的分隔符 | string[] | - | - |
| value | 指定当前选中的条目 | string \| string[] \| number \| number[] \| LabeledValue \| LabeledValue[] | - | - |
| virtual | 设置 false 时关闭虚拟滚动 | boolean | true | - |
| resizable | 设置下拉框是否可 resize | bool \| "vertical" \| "horizontal" | false | 4.5.0 |
| onBlur | 失去焦点时回调 | function | - |
| onChange | 选中 option，或 input 的 value 变化时，调用此函数 | function(value, option:Option \| Array<Option>) | - |
| onClear | 清除内容时回调 | function | - |
| onDeselect | 取消选中时调用 | function(string \| number \| LabeledValue) | - |
| onDropdownVisibleChange | 展开下拉菜单的回调 | function(open) | - |
| onFocus | 获得焦点时回调 | function | - |
| onInputKeyDown | 按键按下时回调 | function | - |
| onMouseEnter | 鼠标移入时回调 | function | - |
| onMouseLeave | 鼠标移出时回调 | function | - |
| onPopupScroll | 下拉列表滚动时的回调 | function | - |
| onSearch | 文本框值变化时回调 | function(value: string) | - |
| onSelect | 被选中时调用 | function(string \| number \| LabeledValue, option: Option) | - |
| onResizeStart | resize 开始时的回调 | function | 4.5.0 |
| onResize | resize 时的回调 | function | 4.5.0 |
| onResizeStop | resize 结束时的回调 | function | 4.5.0 |



### Select实例 方法

| 方法名 | 说明 | 版本 |
|--------|------|------|
| blur() | 取消焦点 | - |
| focus() | 获取焦点 | - |

### Option 属性

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|--------|------|
| className | Option 器类名 | string | - | - |
| disabled | 是否禁用 | boolean | false | - |
| title | 选中该 Option 后，Select 的 title | string | - | - |
| value | 默认根据此属性值进行筛选 | string \| number | - | - |

### OptGroup 属性

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|--------|------|
| key | Key | string | - | - |
| label | 组名 | string \| React.Element | - | - |

## 键盘操作

| 按键 | 功能 |
|------|------|
| ↑(上箭) | 向上切换选项 |
| ↓(下箭) | 向下切换选项 |
| esc | 关闭下拉项 |
| enter | 选中下拉框 |

## 自动化测试

### fieldid 场景说明

| 场景 | 生成规则 | 版本 |
|------|----------|------|
| 根元素 | fieldid | 4.3.0 |
| 输入框 | fieldid + "_search_input" | 4.3.0 |
| 下拉箭头 | fieldid + "_suffix" | 4.3.0 |
| 多选已选选项 | fieldid + "_tag_${index}" | 4.3.0 |
| 多选已选选项删除图标 | fieldid + "_remove_${index}" | 4.3.0 |
| 下拉选项 | fieldid + "_option_${index}" | 4.3.0 |
| 多选下拉选项已选图标 | fieldid + "_item_selected" | 4.3.0 |
| 清空图标 | fieldid + "_clear" | 4.3.0 |

## 常见问题

### 1. 使用 options 属性需要注意什么？

如果传递 options 属性来生成 Option，之前的版本我们用 key 属性渲染文字，现在需要使用 label 属性来渲染文字，否则，将通过 value 渲染文字。

### 2. 使用 getPopupContainer 属性需要注意什么？

不要将 Select 渲染的父节点设置为 Modal 外层的 DOM 元素，如果设置到外层的元素(.wui-modal 或者.wui-modal-dialog)，会出现选项不可点击的情况。可以设置到 wui-modal-content 上。

### 3. 为什么在滚动过程中数据出现渲染异常（重复，错乱）？

1. 检查一下 Option 组件的 key 是否有重复。
2. 检查一下外层传入数据的组件两次 render 的数据是否一致。

### 4. 为什么 focus()方法不生效？

页面中有其他获得了焦点的元素。

## 废弃属性

以下属性已被废弃，请使用新的替代方案：

| 废弃属性 | 替代方案 | 说明 |
|----------|----------|------|
| data | options | 请使用 options 代替，可以设置 data 属性来自动生成 option |
| multiple | mode | 请使用 mode 代替，支持多选 |
| tags | mode | 请使用 mode 代替，可以把随意输入的条目作为 tag |
| supportWrite | mode="combobox" | 请使用 mode="combobox"代替，mode 设置为 combobox 的下拉框，可以输入字符串获得 Select 的值 |

