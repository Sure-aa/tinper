---
tags:
  - TinperNext
  - treeselect组件
---
# 树选择 TreeSelect

类似 Select 的选择控件，可选择的数据结构是一个树形结构时，可以使用 TreeSelect，例如公司层级、学科系统、分类目录等等。

## 组件特性

- 支持单选、多选
- 支持树形数据展示
- 支持搜索过滤
- 支持异步加载
- 支持自定义节点
- 支持虚拟滚动
- 支持可调整大小


## API

### TreeSelect 属性

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|--------|------|
| allowClear | 显示清除按钮 | boolean | false | - |
| autoClearSearchValue | 当多选模式下值被选择，自动清空搜索框 | boolean | true | - |
| requiredStyle | 必填样式 | Boolean | false | 4.6.6 |
| bordered | 设置边框，支持无边框、下划线模式 | `boolean` \| `bottom` | - | 4.5.2 |
| align | 设置文本对齐方式 | `left` \| `center` \| `right` | - | 4.5.2 |
| defaultValue | 指定默认选中的条目 | string \| string[] | - | - |
| disabled | 是否禁用 | boolean | false | - |
| readOnly | 是否只读 | boolean | false | 15.5.x |
| popupClassName | 下拉菜单的 className 属性 | string | - | - |
| dropdownMatchSelectWidth | 下拉菜单和选择器同宽 | boolean \| number | true | - |
| dropdownRender | 自定义下拉框内容 | (originNode: ReactNode, Footer) => ReactNode | - | - |
| dropdownStyle | 下拉菜单的样式 | object | - | - |
| fieldNames | 自定义节点 label、value、children 的字段 | object | { label: 'label', value: 'value', children: 'children' } | 4.2.1 |
| filterTreeNode | 是否根据输入项进行筛选 | boolean \| function(inputValue: string, treeNode: TreeNode) | function | - |
| getPopupContainer | 菜单渲染父节点 | function(triggerNode) | () => document.body | - |
| labelInValue | 是否把每个选项的 label 包装到 value 中 | boolean | false | - |
| listHeight | 设置弹窗滚动高度 | number | 200 | - |
| loadData | 异步加载数据 | function(node) | - | - |
| maxTagCount | 最多显示多少个 tag | number \| `responsive` | - | - |
| maxTagPlaceholder | 隐藏 tag 时显示的内容 | ReactNode \| function(omittedValues) | - | - |
| multiple | 支持多选 | boolean | false | - |
| notFoundContent | 设定搜索不到数据显示的内容 | String | '无匹配结果' | - |
| placeholder | 选择框默认文字 | string | - | - |
| placement | 选择框弹出的位置 | `bottomLeft` \| `bottomRight` \| `topLeft` \| `topRight` | bottomLeft | 4.2.1 |
| searchValue | 搜索框的值 | string | - | - |
| showArrow | 是否显示 `suffixIcon` | boolean | - | - |
| showCheckedStrategy | 配置选中项回填的方式 | `TreeSelect.SHOW_ALL` \| `TreeSelect.SHOW_PARENT` \| `TreeSelect.SHOW_CHILD` | `TreeSelect.SHOW_CHILD` | - |
| showSearch | 是否支持搜索框 | boolean | 单选：false \| 多选：true | - |
| size | 选择框大小 | string | large / middle / small | - |
| suffixIcon | 自定义的选择框后缀图标 | ReactNode | - | - |
| switcherIcon | 自定义树节点的展开/折叠图标 | ReactNode | - | - |
| tagRender | 自定义 tag 内容 | (props) => ReactNode | - | 4.2.1 |
| treeCheckable | 显示 Checkbox | boolean | false | - |
| treeCheckStrictly | 节点选择完全受控 | boolean | false | - |
| treeData | treeNodes 数据 | array<{value, title, children, [disabled, disableCheckbox, selectable, checkable]}> | [] | - |
| treeDataSimpleMode | 使用简单格式的 treeData | boolean \| object<{ id: string, pId: string, rootPId: string }> | false | - |
| treeDefaultExpandAll | 默认展开所有树节点 | boolean | false | - |
| treeDefaultExpandedKeys | 默认展开的树节点 | string[] | - | - |
| treeExpandedKeys | 设置展开的树节点 | string[] | - | - |
| treeIcon | 是否展示 TreeNode title 前的图标 | boolean | false | - |
| treeNodeFilterProp | 输入项过滤对应的 treeNode 属性 | string | `value` | - |
| treeNodeLabelProp | 作为显示的 prop 设置 | string | `title` | - |
| value | 指定当前选中的条目 | string \| string[] | - | - |
| virtual | 设置 false 时关闭虚拟滚动 | boolean | true | - |
| resizable | 设置下拉框是否可 resize | bool \| "vertical" \| "horizontal" | false | - |
| fieldid | 自动化测试专用属性 | string | - | 4.3.0 |
| onChange | 选中树节点时调用此函数 | function(value, label, extra) | - |
| onDropdownVisibleChange | 展开下拉菜单的回调 | function(open) | - |
| onSearch | 文本框值变化时回调 | function(value: string) | - |
| onSelect | 被选中时调用 | function(value, option) | - |
| onTreeExpand | 展示节点时调用 | function(expandedKeys) | - |
| onResizeStart | resize 开始时的回调 | function | - |
| onResize | resize 时的回调 | function | - |
| onResizeStop | resize 结束时的回调 | function | - |


### TreeSelect实例 方法

| 方法名 | 说明 | 版本 |
|--------|------|------|
| blur() | 移除焦点 | - |
| focus() | 获取焦点 | - |

### TreeNode 属性

> 建议使用 treeData 来代替 TreeNode，免去手工构造麻烦

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|------|------|------|--------|------|
| checkable | 当树为 Checkbox 时，设置独立节点是否展示 Checkbox | boolean | - | - |
| disableCheckbox | 禁掉 Checkbox | boolean | false | - |
| disabled | 是否禁用 | boolean | false | - |
| isLeaf | 是否是叶子节点 | boolean | false | - |
| key | 此项必须设置（其值在整个树范围内唯一） | string | - | - |
| selectable | 是否可选 | boolean | true | - |
| title | 树节点显示的内容 | ReactNode | `---` | - |
| value | 默认根据此属性值进行筛选 | string | - | - |

## 自动化测试

### fieldid 场景说明

| 场景 | 生成规则 | 版本 |
|------|----------|------|
| 根元素 | fieldid | 4.3.0 |
| 树节点 | fieldid + "_option_${index}" | 4.3.0 |
| 展开折叠按钮 | fieldid + "_treeselect_switcher" | 4.3.0 |
| 下拉箭头 | fieldid + "_suffix_icon" | 4.3.0 |

## 常见问题

### 1. 为什么渲染树的层级会发生错乱，比如数组中同一级别的数据渲染出了缩进效果？

检查一下数据中的 value，保证唯一性，同样的 value 出现在不同的父级子级中会渲染出错误的树结构。

## 废弃属性

以下属性已被废弃，请使用新的替代方案：

| 废弃属性 | 替代方案 | 说明 |
|----------|----------|------|
| dropdownClassName | popupClassName | 请使用 popupClassName 代替 |

