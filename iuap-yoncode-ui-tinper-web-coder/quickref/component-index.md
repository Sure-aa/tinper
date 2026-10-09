# 完整组件索引

## Pro 组件（tne-tinpernextpro-fe）— 24 个

| 组件 | 说明 | 文档 |
| --- | --- | --- |
| DataForm | 自适应布局数据表单，22 种 inputType，编辑/浏览态 | `../references/DataForm/readme.md` |
| SearchForm | 查询表单，折叠/已选条件/实时搜索 | `../references/SearchForm/readme.md` |
| TinperGrid | 原始 Grid 组件（@tinper/grid），无业务封装，完整 Grid API，适合深度定制 | `../references/TinperGrid/readme.md` |
| DataGrid | 数据网格（新），直接基于 @tinper/grid，原生 Grid API + 业务能力 | `../references/DataGrid/readme.md` |
| EditGrid | 编辑表格（新），直接基于 @tinper/grid，原生 Grid API + 编辑能力 | `../references/EditGrid/readme.md` |
| GridCompat（导出名 Table） | 兼容表格：Grid 渲染 + wui-table API，**存量迁移专用**，新项目用 DataGrid | `../references/GridCompat/readme.md` |
| DataTable | 数据网格（旧），内置分页请求/排序筛选/操作列 | `../references/DataTable/readme.md` |
| EditTable | 行内编辑表格（旧），10+ editType | `../references/EditTable/readme.md` |
| RefTable | 参照穿梭选择，单选/多选/搜索/分页 | `../references/RefTable/readme.md` |
| TableTransfer | 左右双表格穿梭框 | `../references/TableTransfer/readme.md` |
| GroupCascader | 分组级联选择器 | `../references/GroupCascader/readme.md` |
| InputSelect | 下拉表格搜索选择 | `../references/InputSelect/readme.md` |
| Editor | 基于 TinyMCE 的富文本编辑器 | `../references/Editor/readme.md` |
| Email | 邮箱输入，域名提示+格式校验 | `../references/Email/readme.md` |
| Phone | 电话输入，区号/主机号/分机号 | `../references/Phone/readme.md` |
| Mobile | 手机号输入，国际区号 | `../references/Mobile/readme.md` |
| Identity | 证件号输入，多种证件类型 | `../references/Identity/readme.md` |
| InputMultilang | 多语言文本输入 | `../references/InputMultilang/readme.md` |
| Map | 地图选点/地址录入，高德/百度/谷歌三服务商统一 API | `../references/Map/readme.md` |
| LeftMenu | 应用侧边导航菜单 | `../references/LeftMenu/readme.md` |
| Link | 链接编辑/浏览态 | `../references/Link/readme.md` |
| ProConfigProvider | Pro 全局配置（语言/主题/布局） | `../references/ProConfigProvider/readme.md` |
| PageGuide | 页面功能引导 | `../references/PageGuide/readme.md` |
| StepGuide | 分步骤操作引导 | `../references/StepGuide/readme.md` |

## Pro Layouts（tne-tinpernextpro-fe/layouts）

| 组件 | 说明 | 文档 |
| --- | --- | --- |
| ListLayout | 列表页布局容器，子组件流式平铺 | `../references/layouts/ListLayout.md` |
| DetailLayout | 详情页布局容器，带 Header/Footer 静态子组件 | `../references/layouts/DetailLayout.md` |
| LineTabs | fill-line 子表页签，基于 TinperNext Tabs | `../references/layouts/LineTabs.md` |
| ToolbarLayout | 工具栏布局，支持左/中/右/两端对齐 | `../references/layouts/ToolbarLayout.md` |
| TreeTableLayout | 左树右表或左树右卡片布局 | `../references/layouts/TreeTableLayout.md` |

## Pro 支撑服务（tne-tinpernextpro-fe/supports）

| 能力 | 说明 | 文档 |
| --- | --- | --- |
| approval | 审批运行时、审批实例、字段权限 | `../references/supports/approval.md` |
| autoCode | 自动编码规则查询和取号 | `../references/supports/autoCode.md` |
| draft | 草稿保存、草稿管理、草稿列表 | `../references/supports/draft.md` |
| mdfFilter | MDF 过滤面板渲染和条件读取 | `../references/supports/mdfFilter.md` |
| mdfRefer | MDF 参照、范围过滤、runtime 加载 | `../references/supports/mdfRefer.md` |
| print | 打印预览、直接打印、打印次数校验 | `../references/supports/print.md` |
| upload | 上传组件、附件 session、临时附件绑定 | `../references/supports/upload.md` |

## 基础组件（@tinper/next-ui）— 63 个

**基础**: Button、Icon、Typography

**布局**: Layout(Row/Col/Sider/Content/Spliter)、Space、Divider、Card、List

**数据录入**: Form、Input(含 TextArea/Search/Password)、InputNumber、InputGroup、Select、Checkbox、Radio、Switch、DatePicker(含 RangePicker)、TimePicker、Upload(含 Dragger)、TreeSelect、Cascader、Slider、Rate、ColorPicker、AutoComplete

**数据展示**: Table(含 HOC multiSelect/dragColumn/bigData/singleFilter/sort/sum)、Tree、Tabs、Collapse、Tag、Badge、Timeline

**反馈**: Modal(含命令式 confirm/info/success/warning/error)、Drawer、Message、Notification、Spin、Alert、Popconfirm、Popover、Tooltip、Progress、Skeleton

**导航**: Menu、Breadcrumb、Pagination、Steps、Dropdown、Transfer

**其他**: Affix、Anchor、BackTop、Avatar、Image、Calendar、Carousel、Empty、ErrorMessage、Clipboard、SvgIcon、ButtonGroup、Locale、Provider

所有基础组件文档路径: `../references/wui-组件名/api.md`
