# 需求 → 组件路由表（"我想做 X，该用什么？"）

## 表单 / 数据录入类

| 需求描述 | 推荐组件 | 关键属性 | 包 | 文档 |
| --- | --- | --- | --- | --- |
| 列表页搜索条件区 | SearchForm | `formLayout={4}` `collapsedNumber={1}` 根属性 `onSearch` `onReset`，`submitter` 仅定制按钮区 | Pro | `../references/SearchForm/readme.md` |
| 新增/编辑/详情表单页 | DataForm | `formLayout="auto"` `formMode="edit"/"browse"` `labelWidth` | Pro | `../references/DataForm/readme.md` |
| 简单表单（字段少、无复杂布局） | Form | `layout` `onFinish` `Form.Item` + `rules` | Base | `../references/wui-form/api.md` |
| 文本输入 | Input | `value` `onChange` `maxLength` `placeholder` `allowClear` | Base | `../references/wui-input/api.md` |
| 多行文本 | Input.TextArea | `autoSize={{minRows:2,maxRows:6}}` `maxLength` | Base | `../references/wui-input/api.md` |
| 搜索输入框 | Input.Search | `onSearch` `enterButton` `loading` `allowClear` | Base | `../references/wui-input/api.md` |
| 密码输入 | Input.Password | `visibilityToggle` `iconRender` | Base | `../references/wui-input/api.md` |
| 数字输入 | InputNumber | `min` `max` `precision` `step` | Base | `../references/wui-input-number/api.md` |
| 单选下拉 | Select | `options` `onChange` `allowClear` `placeholder` | Base | `../references/wui-select/api.md` |
| 多选下拉 | Select | `mode="multiple"` `options` `maxTagCount` | Base | `../references/wui-select/api.md` |
| 可搜索下拉 | Select | `showSearch` `filterOption` 或 `onSearch` | Base | `../references/wui-select/api.md` |
| 树形下拉选择 | TreeSelect | `treeData` `onChange` `showSearch` | Base | `../references/wui-treeselect/api.md` |
| 级联选择 | Cascader | `options` `onChange` `loadData` | Base | `../references/wui-cascader/api.md` |
| 日期选择 | DatePicker | `format` `showTime` `picker` `onChange` | Base | `../references/wui-datepicker/api.md` |
| 日期范围选择 | DatePicker.RangePicker | `format` `onChange` | Base | `../references/wui-datepicker/api.md` |
| 时间选择 | TimePicker | `format` `onChange` | Base | `../references/wui-timepicker/api.md` |
| 单选按钮组 | Radio / Radio.Group | `options` `onChange` `optionType="button"` | Base | `../references/wui-radio/api.md` |
| 多选复选框 | Checkbox / Checkbox.Group | `options` `onChange` | Base | `../references/wui-checkbox/api.md` |
| 开关 | Switch | `checked` `onChange` `checkedChildren` | Base | `../references/wui-switch/api.md` |
| 文件上传 | Upload / Upload.Dragger | `action` `fileList` `onChange` `beforeUpload` `accept` | Base | `../references/wui-upload/api.md` |
| 滑块 | Slider | `min` `max` `step` `onChange` | Base | `../references/wui-slider/api.md` |
| 评分 | Rate | `count` `onChange` `allowHalf` | Base | `../references/wui-rate/api.md` |
| 颜色选择 | ColorPicker | `value` `onChange` | Base | `../references/wui-colorpicker/api.md` |
| 自动补全 | AutoComplete | `options` `onSearch` `onChange` | Base | `../references/wui-autocomplete/api.md` |
| 邮箱输入（带域名提示） | Email | `check` `emailDomainList` | Pro | `../references/Email/readme.md` |
| 电话输入（区号+主机号+分机号） | Phone | `value={{H,E}}` `cityCode` | Pro | `../references/Phone/readme.md` |
| 手机号输入（国际区号） | Mobile | `countryCode` `validate` | Pro | `../references/Mobile/readme.md` |
| 证件号输入 | Identity | `value={{idType,identity}}` `idTypes` | Pro | `../references/Identity/readme.md` |
| 多语言文本输入 | InputMultilang | `locale` `localeList` `onOk` | Pro | `../references/InputMultilang/readme.md` |
| 富文本编辑 | Editor | `onUpload` `init.plugins` `init.toolbar` | Pro | `../references/Editor/readme.md` |
| 下拉表格搜索选择 | InputSelect | `columns` `dataSource` `multiple` | Pro | `../references/InputSelect/readme.md` |
| 分组级联选择 | GroupCascader | `options` `loadDataFlag` `showSearch` | Pro | `../references/GroupCascader/readme.md` |
| 地图选点 / 地址录入（高德/百度/谷歌） | Map | `mapType` `value` `onChange` `amapKey`/`baiduMapKey`/`googleMapKey` | Pro | `../references/Map/readme.md` |

## 表格 / 数据展示类

> 选型前先判断「改动已有表格 还是 新建表格」（见 `../rules/selection-rules.md` 决策 0）。
> 改动已有表格：保持原组件不替换。新建表格：优先 Grid 系列，仅用户明确指定才用 DataTable/EditTable/Table。

| 需求描述 | 首选组件 | 备选（仅用户指定） | 关键属性 | 包 | 文档 |
| --- | --- | --- | --- | --- | --- |
| 列表页标准数据网格（新建） | DataGrid | DataTable | `columnDefs` `data` `pagination` `rowSelection` `operations` | Pro | `../references/DataGrid/readme.md` |
| 可行内编辑/子表/明细/增删行（新建） | EditGrid | EditTable | `editMode="inline"/"expandForm"` `columnDefs[].editor` `editTrigger` | Pro | `../references/EditGrid/readme.md` |
| 用户明确说明需要基础/普通表格、或按需引入 Grid 模块（新建） | TinperGrid | Table | `columnDefs` `data` `onReady` `modules` | Pro | `../references/TinperGrid/readme.md` |
| 大数据 / 冻结列 / 拖拽列 / 复杂业务表格（新建） | DataGrid | DataTable / Table+HOC | `columnDefs` `data` `pagination` | Pro | `../references/DataGrid/readme.md` |
| 改动项目已有表格（任意类型） | 保持原组件 | — | 直接在原表上改，不替换 | — | 原组件对应文档 |
| 用户明确要求用旧数据表格 | DataTable | — | `columns` `request` `pagination` `rowSelection` `operationItems` | Pro | `../references/DataTable/readme.md` |
| 用户明确要求用旧编辑表格 | EditTable | — | `type="inline"/"inlineForm"` `columns[].editType` `editAbled` | Pro | `../references/EditTable/readme.md` |
| 用户明确要求纯展示 Base 表格 | Table | — | `data` `columns` `rowKey` `bordered` `scroll` | Base | `../references/wui-table/api.md` |
| 表格多选行（Base Table） | Table + HOC `multiSelect` | — | `multiSelect(Table,Checkbox)` → `rowSelection` | Base | `../references/wui-table/api.md` |
| 表格列可拖拽调整宽度（Base Table） | Table + HOC `dragColumn` | — | `dragColumn(Table)` → `dragborder` `onDropBorder` | Base | `../references/wui-table/api.md` |
| 大数据虚拟滚动（Base Table） | Table + HOC `bigData` | — | `bigData(Table)` → `scroll={{y:500}}` | Base | `../references/wui-table/api.md` |
| 表格列筛选（Base Table） | Table + HOC `singleFilter` | — | `singleFilter(Table)` | Base | `../references/wui-table/api.md` |
| 多个 HOC 链式组合（Base Table） | `dragColumn(bigData(multiSelect(Table,Checkbox)))` | — | 外层包内层 | Base | `../references/wui-table/api.md` |
| 把旧 wui-table / 旧 Table 升级到高性能虚拟滚动 Grid（存量迁移，用户明确要求） | GridCompat（导出名 Table） | DataGrid（新建推荐直接用） | `columns` `compatConfig` `enableSorting` `rowSelection` | Pro | `../references/GridCompat/readme.md` |
| 参照弹窗选择（单选/多选穿梭） | RefTable | — | `type="radio"/"checkbox"` `columns` `data` `fieldNames` `labelInValue` | Pro | `../references/RefTable/readme.md` |
| 左右双表格穿梭框 | TableTransfer | — | `leftColumns` `rightColumns` `data` `rowKey` | Pro | `../references/TableTransfer/readme.md` |
| 简单列表穿梭 | Transfer | — | `dataSource` `targetKeys` `onChange` `render` | Base | `../references/wui-transfer/api.md` |
| 分页 | Pagination | — | `current` `pageSize` `total` `onChange` | Base | `../references/wui-pagination/api.md` |
| 树形数据展示 | Tree | — | `treeData` `defaultExpandAll` `onSelect` `checkable` | Base | `../references/wui-tree/api.md` |

## 反馈 / 弹出层类

| 需求描述 | 推荐组件 | 关键属性 | 包 | 文档 |
| --- | --- | --- | --- | --- |
| 弹窗（自定义内容） | Modal 声明式 | `visible` `onOk` `onCancel` `width` `title` `destroyOnClose` | Base | `../references/wui-modal/api.md` |
| 确认弹窗 | Modal.confirm() | `title` `content` `onOk` `onCancel` | Base | `../references/wui-modal/api.md` |
| 信息提示弹窗 | Modal.info()/success()/warning()/error() | `title` `content` `onOk` | Base | `../references/wui-modal/api.md` |
| 侧边抽屉 | Drawer | `visible` `placement` `width` `title` `onClose` | Base | `../references/wui-drawer/api.md` |
| 轻量成功/失败提示 | Message | `Message.success()` `.error()` `.warning()` `.create()` | Base | `../references/wui-message/api.md` |
| 通知提醒（右上角角标） | Notification | `Notification.open()` `.success()` `.error()` | Base | `../references/wui-notification/api.md` |
| 警告提示（页内常驻） | Alert | `type` `message` `description` `closable` `showIcon` | Base | `../references/wui-alert/api.md` |
| 加载中状态 | Spin | `spinning` `tip` `delay` | Base | `../references/wui-spin/api.md` |
| 气泡确认框 | Popconfirm | `content` `onClose` `onCancel` | Base | `../references/wui-popconfirm/api.md` |
| 文字提示 | Tooltip | `overlay` `placement` `trigger` | Base | `../references/wui-tooltip/api.md` |
| 气泡卡片 | Popover | `content` `title` `placement` `trigger` | Base | `../references/wui-popover/api.md` |
| 进度条 | Progress | `percent` `type` `status` `strokeColor` | Base | `../references/wui-progress/api.md` |
| 骨架屏 | Skeleton | `loading` `avatar` `paragraph` `title` | Base | `../references/wui-skeleton/api.md` |
| 空状态 | Empty | `description` `image` | Base | `../references/wui-empty/api.md` |
| 错误信息展示 | ErrorMessage | `ErrorMessage.create({message,errorInfo,footer})` | Base | `../references/wui-error-message/api.md` |
| 行内复制 | Clipboard | `action="copy"` `text` `success` | Base | `../references/wui-clipboard/api.md` |

## 页面结构 / 导航 / 其他类

| 需求描述 | 推荐组件 | 关键属性 | 包 | 文档 |
| --- | --- | --- | --- | --- |
| 按钮操作 | Button | `type="primary"` `colors="danger"` `loading` `disabled` `onClick` | Base | `../references/wui-button/api.md` |
| 按钮组 | ButtonGroup | 包裹多个 Button | Base | `../references/wui-button-group/api.md` |
| 工具栏/按钮间距排列 | Space | `direction="horizontal"` `size` `wrap` | Base | `../references/wui-space/api.md` |
| 标签页切换 | Tabs + TabPane | `activeKey` `onChange` `type="line"/"card"` | Base | `../references/wui-tabs/api.md` |
| 折叠面板 | Collapse + Panel | `activeKey` `onChange` `accordion` | Base | `../references/wui-collapse/api.md` |
| 标签/标记 | Tag | `color="success"/"warning"/"danger"` `closable` `select` | Base | `../references/wui-tag/api.md` |
| 徽标/角标 | Badge | `count` `dot` `offset` | Base | `../references/wui-badge/api.md` |
| 面包屑导航 | Breadcrumb | `separator` `Breadcrumb.Item` | Base | `../references/wui-breadcrumb/api.md` |
| 菜单导航 | Menu + SubMenu + Item | `mode` `selectedKeys` `onSelect` | Base | `../references/wui-menu/api.md` |
| 步骤条 | Steps + Step | `current` `status` `type` | Base | `../references/wui-steps/api.md` |
| 下拉菜单 | Dropdown | `overlay`(Menu) `trigger` | Base | `../references/wui-dropdown/api.md` |
| 时间线 | Timeline + Item | `color` `dot` | Base | `../references/wui-timeline/api.md` |
| 列表页页面骨架（查询区 + 工具栏 + 表格） | ListLayout | `children` | Pro layouts | `../references/layouts/ListLayout.md` |
| 详情页页面骨架（头部 + 表单 + 底部操作） | DetailLayout | `DetailLayout.Header` `DetailLayout.Footer` | Pro layouts | `../references/layouts/DetailLayout.md` |
| 子表页签 / 明细页签 | LineTabs | `items` `extra` `activeKey` `onChange` | Pro layouts | `../references/layouts/LineTabs.md` |
| 工具栏按钮对齐 | ToolbarLayout | `align="left"/"center"/"right"/"between"` | Pro layouts | `../references/layouts/ToolbarLayout.md` |
| 左树右表 / 左树右卡片 | TreeTableLayout | `tree` `content` `treeWidth` `contentKind` | Pro layouts | `../references/layouts/TreeTableLayout.md` |
| 栅格布局 | Row + Col | `Row.gutter` `Col.span` `Col.xs/sm/md/lg/xl` | Base | `../references/wui-layout/api.md` |
| 页面布局 | Layout + Sider + Content | `Sider.width` `Layout.Spliter`(可拖拽调节) | Base | `../references/wui-layout/api.md` |
| 卡片容器 | Card | `title` `extra` `bordered` `actions` | Base | `../references/wui-card/api.md` |
| 列表 | List | `dataSource` `renderItem` `pagination` | Base | `../references/wui-list/api.md` |
| 分割线 | Divider | `type` `orientation` `dashed` | Base | `../references/wui-divider/api.md` |
| 回到顶部 | BackTop | `visibilityHeight` `onClick` | Base | `../references/wui-backtop/api.md` |
| 固钉 | Affix | `offsetTop` `onChange` | Base | `../references/wui-affix/api.md` |
| 锚点导航 | Anchor | `items` `onClick` | Base | `../references/wui-anchor/api.md` |
| 头像 | Avatar | `size` `src` `icon` `shape` | Base | `../references/wui-avatar/api.md` |
| 图片 | Image | `src` `alt` `preview` `fallback` | Base | `../references/wui-image/api.md` |
| 排版文本 | Typography | `Typography.Paragraph` `ellipsis`（注意：无 Title/Text 子组件） | Base | `../references/wui-typography/api.md` |
| 日历 | Calendar | `value` `onChange` `fullscreen` | Base | `../references/wui-calendar/api.md` |
| 走马灯/轮播 | Carousel | `autoplay` `dots` `afterChange` | Base | `../references/wui-carousel/api.md` |
| 图标 | Icon | `type="uf-xxx"` | Base | `../references/wui-icon/api.md` |
| SVG 图标 | SvgIcon | `component` `name` | Base | `../references/wui-svgicon/api.md` |
| 全局配置 | ConfigProvider | `locale` | Base | `../references/wui-provider/api.md` |
| 国际化 | Locale | `Locale.getLocale()` | Base | `../references/wui-locale/api.md` |
| Pro 全局配置 | ProConfigProvider | `locale` `theme` | Pro | `../references/ProConfigProvider/readme.md` |
| 页面引导 | PageGuide | — | Pro | `../references/PageGuide/readme.md` |
| 步骤引导 | StepGuide | — | Pro | `../references/StepGuide/readme.md` |
| 左侧菜单 | LeftMenu | `headerConfig` `menuConfig` | Pro | `../references/LeftMenu/readme.md` |
| 链接编辑/浏览态 | Link | — | Pro | `../references/Link/readme.md` |
