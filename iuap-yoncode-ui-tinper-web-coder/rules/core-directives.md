# 核心指令（必须遵守）

1. **禁止编造**: 不凭记忆或猜测回答，**必须先读取本地文档**再回答
2. **本地文档优先**: 详细 API 和示例在 `../references/` 目录
3. **优先用 Pro 组件**: 企业场景下 Pro 组件封装更完善，优先推荐（但需先走选型决策表确认适用场景）
4. **仅使用 ynpm 安装**: TinperNext 已不再维护 npm 公共镜像源，**禁止**使用 npm/cnpm 安装或查询版本，**必须**使用 ynpm
   - TNS 只用于运行时动态加载和托管组件资源；需要写入本地 `node_modules`、查询本地依赖版本或执行源码查证时使用 ynpm 安装。
5. **正确理解 API 表格中的"版本"列**: "版本"表示该 API/属性首次支持的组件库版本（`since`），**不是**推荐版本或当前项目安装版本
6. **回答兼容性问题时做版本映射**: 先区分 Base/Pro 组件，再将 API 表格中的"版本"与项目实际安装版本比较
7. **源码查证触发条件**: 默认先读 `../references/`；只有文档缺失/矛盾/不够时才读 `node_modules/`
8. **源码读取范围**: Base 组件读 `node_modules/@tinper/next-ui/`；Pro 组件读 `node_modules/tne-tinpernextpro-fe/`
9. **源码读取方式**: 优先用 rg 定位；先看 package.json、入口文件、类型声明
10. **实际版本判断**: 先读项目声明版本和已安装包版本，API 表格用于说明 `since`
11. **选型决策优先**: 同一需求有多种组件可选时，必须先查阅 `./selection-rules.md` 再推荐
12. **表格选型先判断「改动已有」还是「新建」**: 遇到任何表格需求，先走 `./selection-rules.md` 决策 0 算法。① 用户明确指定组件则听用户；② 在项目已有表格上改动 → 保持原组件类型，**禁止**把 `@tinper/next-ui Table`/`DataTable`/`EditTable` 替换为 Grid 系列；③ 新建表格 → 可编辑/子表/明细/增删行优先 **EditGrid**，基础/普通表格优先 **TinperGrid**，其余优先 **DataGrid**（难判时优先 DataGrid）；④ 仅当用户明确要求才用 `@tinper/next-ui Table`/`DataTable`/`EditTable`/`wui-table`。子表、明细表、行内编辑、增删行等关键词**不要默认选 EditTable**
12. **禁止二次封装**: 严禁推荐创建 Wrapper 组件包裹 TinperNext 组件（如 NewModal、BaseTable、CommonForm），直接使用原始组件。重复逻辑用工具函数抽取（如关闭保护用 `confirmBeforeClose` 函数），不抽取 UI 组件
13. **Modal 双模式**: 确认/提示用命令式 `Modal.confirm()/info()/success()/warning()/error()`；复杂内容（含表单/表格）用声明式 `<Modal visible={} onOk={} onCancel={}>`
14. **Form API 风格**: 函数组件用 `Form.useForm()` Hook 式；DataForm/SearchForm 用 `ref={formRef}` 获取实例；不再推荐 `Form.createForm()` HOC 式，除非用户项目已是旧模式
15. **组件搭配一致性**: 同页面已选定 Pro 方案（如用 DataTable），表单部分应同步用 DataForm/SearchForm，不要混用
16. **文档分层读取**: SKILL.md 路由表 → rules/ 指令 → quickref/ 速查 → references/ 组件文档 → references/ demos/ → node_modules/ 源码（仅文档不够时）
17. **visible vs show**: Modal、Drawer 等组件的新代码统一使用 `visible`，禁止使用废弃的 `show`
18. **DataForm inputType 优先**: 使用 DataForm 时优先用内置 inputType（22 种控件类型）声明表单项，不要在 DataForm 内嵌套手写 wui-xxx 组件
19. **数据 key 规则**: 无论 Table/DataTable/EditTable，数据必须含唯一 `key` 字段，建议 `rowKey="id"` 并确保数据有 id
20. **Pro 包名环境差异**: V3R6 环境包名为 `ynf-tinper-next-pro`，非 V3R6 为 `tne-tinpernextpro-fe`
21. **Pro 输入组件可独立使用**: Email、Phone、Mobile、Identity、InputMultilang、Editor、InputSelect、GroupCascader 等 Pro 组件不限于在 DataForm/SearchForm 内使用，可直接在 Form.Item 中作为自定义表单控件独立使用
22. **Typography 仅有 Paragraph**: `Typography.Title` 和 `Typography.Text` 不存在，标题用原生 `<h1>`-`<h6>`，文本用 `<span>`，只有溢出省略场景才用 `Typography.Paragraph`
23. **Carousel 无 autoplaySpeed**: 开启自动播放用 `autoplay`，没有官方的 `autoplaySpeed` 属性
24. **React 18 兼容性警告**: forwardRef 和 defaultProps 警告是组件库内部问题，详见 `../gotchas/react18-compat.md`
25. **Timeline 不支持 items**: 只能用 `<Timeline.Item>` 子组件模式，不支持 `items` 数组属性
26. **DatePicker 使用 Moment**: 不要传 Dayjs 对象，必须用 Moment.js
27. **Select showSearch 类型缺失**: 运行时有效但 TypeScript 类型未声明，需 `@ts-ignore`
28. **Table rowSelection 双路径**: 优先用新 API `rowSelection={{ type, selectedRowKeys, onChange }}`，不要混用旧 `_checked` 字段方式
29. **Message error 映射**: `Message.error()` 内部映射为 `danger` 颜色；另有 `infolight/successlight/dangerlight/warninglight` 独有方法
30. **Pro 包依赖问题**: `tne-tinpernextpro-fe` 将 react 声明为 dependencies 而非 peerDependencies，安装时会产生嵌套 React，必须配置 dedupe/alias/overrides 解决，详见 `../gotchas/pro-install.md`
31. **微前端 getPopupContainer**: 微前端项目中，Modal 命令式弹窗、Select/Cascader/DatePicker 等浮层组件必须传 `getPopupContainer`，防止挂载到 `document.body` 导致沙箱逃逸
32. **DataTable 数据属性用 data**: DataTable 传数据用 `data` 属性，不是 `dataSource`。Base Table 两者都接受（`dataSource` 优先），但统一用 `data` 最安全
33. **DataForm options 平铺传**: DataForm.Item 的 select/radiogroup/checkboxgroup 等类型，选项用 `options={[...]}` 直接传，不要用 EditTable 的 `editOptions` 写法
34. **Popconfirm 用 onClose 不用 onConfirm**: `onConfirm` 已废弃，确认按钮回调统一用 `onClose`；确认消息用 `content`（不是 antd 的 `title`）
35. **Alert closable 默认 true**: 源码默认 `closable={true}`，但企业场景下提示条通常需要 `closable={false}`；用 `type` 而非 `colors` 可传 `"error"`
36. **Tag 表格内用 size="sm"**: 在 Table 列 render 中使用 Tag 展示状态时加 `size="sm"` 保持紧凑
37. **SearchForm onSearch/onReset 在根 props**: `onSearch`/`onReset` 回调直接放在 SearchForm props 上，不是 `submitter.onSearch`；`submitter` 仅用于渲染定制
38. **DataTable reload 是主力 ref 方法**: 真实项目中 DataTable ref 方法几乎只用 `reload([pageNum])`，CRUD/搜索后调用刷新
39. **EditTable editOptions 包裹传**: EditTable 列 select/自定义控件的选项用 `editOptions: { options: [...] }` 对象包裹，不要平铺 `options`（与 DataForm 相反）

---

## NextPro 支撑服务规则

1. **支撑服务先路由**: 遇到审批、草稿、打印、上传、自动编码、MDF 参照、MDF 过滤需求，先查 `../quickref/supports-router.md`
2. **支撑服务文档优先**: 支撑服务 API 以 `../references/supports/` 为准；文档缺失或矛盾时再查 NextPro 源码 `node_modules/tne-tinpernextpro-fe/src/supports/`
3. **优先推荐业务入口**: 不推荐业务侧直接使用支撑服务内部 UI、workbench、dialog、progress 组件，除非 reference 明确列为推荐入口
4. **上下文显式传入**: 业务运行时、request、transport、tenant、domain、billNo、busiObj、facade 方法等必须由业务侧显式传入，不要假设全局 store 或框架对象存在
5. **微前端浮层约束继续生效**: 支撑服务中涉及 Modal、Notification、上传弹窗、MDF 浮层等能力时，仍需处理 `getPopupContainer`

---

## 安装方式

```bash
npm install -g ynpm-tool          # 安装 ynpm
ynpm install @tinper/next-ui      # 安装基础组件
ynpm install tne-tinpernextpro-fe # 安装 Pro 组件
```

```tsx
import { Button, Table, Form, Input, Select, Modal } from '@tinper/next-ui';
import { DataForm, EditTable, SearchForm, RefTable, DataTable, DataGrid, EditGrid } from 'tne-tinpernextpro-fe';
import { Grid } from 'tne-tinpernextpro-fe/TinperGrid';
```

> V3R6 环境包名为 `ynf-tinper-next-pro`，非 V3R6 为 `tne-tinpernextpro-fe`

---

## 页面生成组件优先原则

当任务是"根据设计图生成页面"或"重构现有页面"时：

1. **先找组件，再写结构** — 优先组合 TinperNext/TinperNextPro 组件
2. **只有组件能力明确不覆盖时，才允许回退到自定义 div/span/button**
3. 若 `../references/` 中已有能力覆盖，禁止仅因为"写 div 更快"而跳过组件库
4. 禁止直接用裸结构替代：查询表单、数据表格、编辑表格、卡片容器、标签、标签页、分页、抽屉、模态框、按钮、输入框、选择器、反馈组件
5. 页面生成结束时，说明哪些区域用了组件、哪些没用到及原因

---

## 设计规范触发条件

出现以下情况时，还应读取 `../DESIGN.md` 和 `../designtoken.css`：

- 任务来自设计图/截图/视觉稿
- 需要决定颜色、字号、间距、圆角、阴影
- 涉及样式落地时，优先复用 `designtoken.css` 中已有 `--ynfw-*` / `--wui-*` / `--brand-*` token
