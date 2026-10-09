# 高频组件速查（Top 15）

## Modal（使用频率最高）

**包**: Base | **文档**: `../references/wui-modal/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `visible` | 控制显隐 | state boolean |
| `onOk` | 确定回调 | `(e) => {}` |
| `onCancel` | 取消回调 | `() => setVisible(false)` |
| `width` | 宽度 | `600` / `"80%"` |
| `title` | 标题 | `"编辑"` |
| `destroyOnClose` | 关闭时销毁（默认 `true`） | 需保留状态时设 `false` |
| `maskClosable` | 点击蒙层关闭（默认 `false`，与 antd 相反） | 信息弹窗可设 `true` |
| `okButtonProps` | 确认按钮 props | `{ loading: submitting }` |

命令式: `Modal.confirm({title, content, onOk})` `Modal.success({content})`

## Button

**包**: Base | **文档**: `../references/wui-button/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `type` | 按钮类型 | `"primary"` `"default"` |
| `colors` | 颜色语义 | `"primary"` `"danger"` `"success"` |
| `size` | 大小 | `"sm"` `"md"` |
| `loading` | 加载状态 | `submitting` |
| `disabled` | 禁用 | `!selected` |

## DataGrid（新建列表页/业务表格 首选）

**包**: Pro | **文档**: `../references/DataGrid/readme.md`

> **新建表格时优先 DataGrid**（而非 DataTable）。DataTable 仅用于改动已有表格或用户明确指定时。

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `columnDefs` | 列定义 | `[{field, headerName, width, render, sortable, filter}]` |
| `request` | 数据请求函数 | `({pagination, params}) => Promise<{success, data, total}>` |
| `requestParams` | 查询参数 | `{keyword, status}` — 变化时自动触发重新请求 |
| `pagination` | 分页 | `{current:1, pageSize:10, showTotal: total => \`共 ${total} 条\`}` |
| `rowSelection` | 行选择 | `{mode:'multiRow', selectedRowKeys, onChange: e => setKeys(e.selectedKeys)}` |
| `operations` | 操作列 | `[{key, text, onClick:(record)=>{}, hidden, disabled}]` |
| `operationColumn` | 操作列配置 | `{width:160, pinned:'right'}` 或 `false`（隐藏） |
| `searchPanel` | 搜索区 | `ReactNode`（配合 SearchForm 或自定义） |
| `enableSorting` | 排序 | `true` |
| `enableFilter` | 列筛选 | `true` |
| `enableColumnSet` | 列设置 | `true` |
| `dragborder` | 列宽拖拽 | `true` |
| `showRowNum` | 行号 | `{width:58, pinned:'left'}` |
| `fillSpace` | 填满父容器 | `true` |

Ref 方法: `ref.current.reload()` `.getSelectedRowKeys()` `.getSelectedRows()` `.setSelectedRowKeys(keys)` `.clearSelection()` `.getData()` `.setDataSource(rows)` `.appendRow(row)` `.insertRow(index,row)`

> `reload()` 用当前 `data` 重刷内部 state（不发请求）；数据是外部 `data` 驱动，服务端分页由调用方在 `pagination.onChange` 自取后回填 `data`。

## DataTable（改动已有表格 / 用户明确指定时使用）

**包**: Pro | **文档**: `../references/DataTable/readme.md`

> **不要在新建表格时默认使用 DataTable**，应优先 DataGrid。DataTable 用于：①改动项目已有 DataTable；②用户明确说"用 DataTable"。

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `columns` | 列配置 | `[{title, dataIndex, width, render}]` |
| `request` | 数据请求函数 | `({page:{current,pageSize}, sort, params}) => Promise<{success, data, total}>` |
| `pagination` | 分页 | `{current, pageSize, total, onChange}` |
| `rowSelection` | 行选择 | `{type:'checkbox'}` 或 `false` |
| `operationItems` | 操作列 | `[{key, text, onClick, hidden, rowActivable, otherProps:{disabled}}]` |
| `operationClick` | 操作按钮点击 | `(record, item, e, index) => {}` |
| `operationType` | 操作列样式 | `"button"` `"link"` 或自定义函数 |
| `operationTypeProps` | 操作列配置 | `{maxCount:3, rowActiveKeysMode:'single'/'multiple'/true/false}` |
| `fillSpace` | 填满父容器 | `true` |
| `showRowNum` | 序号列 | `true` 或 `{base:1,width:50}` |
| `rowActiveKeys` | 行点击高亮状态 | `[]` 或 `true` |
| `mode` | 展示模式 | `"table"` `"card"` |
| `showModeSwitch` | 卡片/表格切换 | `true` |
| `isDragColumn` | 列拖拽 | `true`（默认开启） |
| `isSort` | 排序 | `false`（需显式开启） |
| `isBigData` | 大数据渲染 | `false`（需显式开启） |

实例方法: `ref.current.reload([pageNum])` `.getSelectedRowKeys()` `.getSelectedRowData()` `.clearSelectedRowKeys()` `.getDataSource()` `.getQueryFilters()` `.setSelectedRowKeys(keys)` `.clearRowActiveKeys()`

> 真实项目中 `reload()` 是最高频 ref 方法（20+ 处调用），其余方法使用频率较低。

## Select

**包**: Base | **文档**: `../references/wui-select/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `options` | 选项 | `[{label, value}]` |
| `value` | 当前值 | state |
| `onChange` | 选中回调 | `(value) => {}` |
| `showSearch` | 可搜索 | `true` |
| `mode` | 模式 | `"multiple"` / 不设 |
| `allowClear` | 可清除 | `true` |
| `placeholder` | 占位文本 | `"请选择"` |

## Input

**包**: Base | **文档**: `../references/wui-input/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `value` | 当前值 | state |
| `onChange` | 变化回调 | `(e) => setValue(e)` |
| `placeholder` | 占位 | `"请输入"` |
| `maxLength` | 最大长度 | `50` |
| `allowClear` | 可清除 | `true` |
| `onPressEnter` | 回车回调 | 搜索场景 |

子组件: `Input.TextArea` `Input.Search` `Input.Password`

## Space

**包**: Base | **文档**: `../references/wui-space/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `direction` | 方向 | `"horizontal"` |
| `size` | 间距 | `"small"` / `8` / `12` |
| `wrap` | 自动换行 | `true` |

## Icon

**包**: Base | **文档**: `../references/wui-icon/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `type` | 图标名 | `"uf-add"` `"uf-del"` `"uf-search"` `"uf-cloud-o-up"` |
| `style` | 自定义样式 | `{fontSize:16, color:'#1890ff'}` |

## Tooltip

**包**: Base | **文档**: `../references/wui-tooltip/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `overlay` | 提示内容 | `"说明文字"` |
| `placement` | 弹出位置 | `"top"` `"bottom"` `"right"` |
| `trigger` | 触发方式 | `"hover"` `"click"` |

## Spin

**包**: Base | **文档**: `../references/wui-spin/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `spinning` | 是否加载中 | `loading` state |
| `tip` | 提示文字 | `"加载中..."` |
| `delay` | 延迟显示 | `300`（防闪烁） |

## Form

**包**: Base | **文档**: `../references/wui-form/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `form` | 表单实例 | `const [form] = Form.useForm()` |
| `layout` | 布局 | `"horizontal"` `"vertical"` `"inline"` |
| `onFinish` | 提交回调 | `(values) => handleSave(values)` |
| `initialValues` | 初始值 | `{name:''}` |
| `labelCol` | label 布局 | `{span:6}` |

FormItem: `name` `label` `rules={[{required:true, message}]}`

## Tag

**包**: Base | **文档**: `../references/wui-tag/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `color` | 颜色（也接受 `colors`） | 语义: `"success"` `"warning"` `"danger"` `"info"` `"invalid"` `"start"` |
| | | 半透明: `"half-blue"` `"half-green"` `"half-red"` `"half-yellow"` `"half-dark"` |
| `size` | 大小 | `"sm"`（表格内推荐）/ `"md"` / `"lg"` |
| `type` | 填充样式 | `"filled"` / `"bordered"` / `"default"` |
| `closable` | 可关闭 | 筛选条件标签 |
| `select` | 可选择 | 多选标签 |

表格列状态映射: `<Tag size="sm" color={STATUS_MAP[val]?.color}>{STATUS_MAP[val]?.name}</Tag>`

## Tabs

**包**: Base | **文档**: `../references/wui-tabs/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `activeKey` | 当前激活 | state |
| `onChange` | 切换回调 | `(key) => setActiveKey(key)` |
| `type` | 页签样式 | `"line"` `"card"` |

## Collapse

**包**: Base | **文档**: `../references/wui-collapse/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `activeKey` | 展开面板 | state |
| `onChange` | 切换回调 | `(keys) => {}` |
| `accordion` | 手风琴 | `true` |

## DataForm（Pro）

**包**: Pro | **文档**: `../references/DataForm/readme.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `ref` | 表单实例 | `formRef` → `formRef.current.validateFields()` |
| `formLayout` | 列布局 | `"auto"` / `2` / `3` / `4` |
| `formMode` | 编辑/浏览态 | `"edit"` `"browse"` |
| `readOnly` | 全局只读 | `true` |
| `disabled` | 全局禁用 | `true` |
| `hiddenKeys` | 隐藏字段（仍收集） | `["field1"]` 或 `{field:true/false/"visible"/"hidden"}` |
| `invisibleKeys` | 不显示且不收集 | `["field2"]` |
| `requiredKeys` | 必填字段 | `["name","code"]` |
| `disabledKeys` | 禁用字段 | `["id"]` |
| `values` | 受控表单值 | `{name:"xxx"}` |

## usePrint（Pro 支撑服务）

**包**: Pro supports | **文档**: `../references/supports/print.md`

| 参数 | 说明 | 常用值 |
| --- | --- | --- |
| `mode` | 打印场景 | `"card"` / `"list"` |
| `context` | 打印上下文 | `{tenantId,locale,domainKey,appCode,billNo}` |
| `records` | 页面记录 | 卡片模式必填 |
| `selection` | 选中记录 | 列表模式必填 |
| `getRecordId` | 单据 ID 解析 | `row => String(row.id)` |

常用方法: `previewCard()` `printCard()` `previewList()` `printList()`
| `labelWidth` | label 宽度 | `90`（默认） |

DataForm.Item 核心属性: `name` `label` `inputType` `required` `colSpan` `rowBreak` `rules` `pattern` `patternMsg` `readOnly` `disabled` `previewRender`

**inputType 完整枚举（22 种）:**

| inputType | 对应控件 | 常用附加属性 |
| --- | --- | --- |
| `input` | Input | `maxLength` `placeholder` |
| `number` | InputNumber | `min` `max` `precision` `step` |
| `inputNumberGroup` | InputNumberGroup | `placeholder={["最小值","最大值"]}` `rules={[{min,max}]}` |
| `textarea` | Input.TextArea | `autoSize` |
| `search` | Input.Search | `onSearch` |
| `password` | Input.Password | `visibilityToggle` |
| `date` | DatePicker | `format` `showTime` |
| `time` | TimePicker | `format` |
| `rangepicker` | RangePicker | `format` |
| `switch` | Switch | — |
| `select` | Select | `options` `allowClear` |
| `cascader` | Cascader | `options` |
| `radiogroup` | Radio.Group | `options={[{label,value}]}` |
| `checkboxgroup` | Checkbox.Group | `options={[{value,label}]}` |
| `treeselect` | TreeSelect | `treeData` |
| `imageupload` | 图片上传 | `action` |
| `reftree` | 参照树 | 需配置参照信息 |
| `reftable` | 参照表格 | 需配置参照信息 |
| `reftabletree` | 参照表格树 | 需配置参照信息 |
| `custom` | 自定义组件 | `render={()=><Comp/>}`（需遵循 value/onChange 约定） |
| `fileupload` | 附件上传（TODO） | — |
| `inputmap` | 地图选择（TODO） | — |

> `custom` 类型的控件会自动注入 `value`/`onChange`，数据同步由 Form 接管。禁止用 `defaultValue` 设置值，应通过 `initialValues` 或 `setFieldsValue`

## SearchForm（Pro）

**包**: Pro | **文档**: `../references/SearchForm/readme.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `formLayout` | 布局列数 | `4` `"auto"` |
| `collapsedNumber` | 折叠显示行数 | `1` |
| `defaultCollapsed` | 默认折叠 | `true` |
| `onSearch` | 搜索回调 | `(values) => tableRef.current?.reload()` |
| `onReset` | 重置回调 | `() => tableRef.current?.reload()` |
| `submitter` | 按钮区渲染定制 | `{render(props, dom) { return [...dom, extra] }}` 或 `false`（隐藏） |
| `hiddenKeys` | 动态隐藏字段 | `['type', 'name']` |
| `showSelected` | 显示已选条件 | `true` |

> **注意**: `onSearch`/`onReset` 放在 SearchForm props 上，不是 `submitter.onSearch`/`submitter.onReset`。`submitter` 仅用于渲染定制。

SearchForm.Item: `name` `label` `inputType="select"/"input"/"search"/"radiogroup"/"date"/"custom"` `options`

## Upload

**包**: Base | **文档**: `../references/wui-upload/api.md`

| 属性 | 说明 | 常用值 |
| --- | --- | --- |
| `action` | 上传地址 | API URL |
| `fileList` | 文件列表 | state |
| `onChange` | 变化回调 | 标准处理 |
| `beforeUpload` | 上传前校验 | `(file) => checkSize(file)` |
| `accept` | 文件类型 | `".jpg,.png"` |
| `maxCount` | 最大数量 | `5` |

子组件: `Upload.Dragger`（拖拽上传）

## Table + HOC（Base 旧模式）

**包**: Base | **文档**: `../references/wui-table/api.md` 高阶函数章节

| HOC | 说明 | 用法 |
| --- | --- | --- |
| `multiSelect(Table, Checkbox)` | 多选行 | 包裹后支持 `rowSelection` |
| `dragColumn(Table)` | 列宽拖拽 | 包裹后支持 `dragborder` `onDropBorder` |
| `bigData(Table)` | 大数据虚拟滚动 | 包裹后配合 `scroll={{y:500}}` |
| `singleFilter(Table)` | 单列筛选 | 包裹后列配置加 `filterType` |
| `sort(Table)` | 排序 | 包裹后列配置加 `sorter` |
| `sum(Table)` | 合计行 | 包裹后列配置加 `sumCol` |

链式组合: `dragColumn(bigData(multiSelect(Table, Checkbox)))` → 外层包内层

> 新建表格优先 DataGrid（内置拖拽列/排序/大数据能力）；仅当用户明确要求用 Base Table 灵活组合时才用 Table + HOC。改动已有 Table 则保持原组件不替换。
