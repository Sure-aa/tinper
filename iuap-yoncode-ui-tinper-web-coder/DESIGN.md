---
version: alpha
name: Tinper Web Enterprise
description: 源自 designtoken.css 的 TinperNext 与 TinperNextPro 企业级 Web 设计系统。
colors:
  primary: "#e60012"
  primary-hover: "#c2000f"
  primary-pressed: "#9e000c"
  primary-light: "#ffcfd3"
  primary-disabled: "#ff959d"
  text-primary: "#111827"
  text-secondary: "#374151"
  text-tertiary: "#6b7280"
  text-disabled: "#9ca3af"
  text-inverse: "#ffffff"
  background: "#ffffff"
  background-muted: "#f9fafb"
  background-hover: "#e5e7eb"
  background-selected: "#dbeafe"
  background-selected-hover: "#d1d5db"
  background-searchform: "#f8fafc"
  border: "#d1d5db"
  border-hover: "#4b5563"
  border-light: "#f3f4f6"
  border-disabled: "#e5e7eb"
  focus: "#1d4ed8"
  link: "#1d4ed8"
  link-hover: "#3b82f6"
  success: "#10b981"
  success-light: "#f0fdf4"
  warning: "#f59e0b"
  warning-light: "#fffbeb"
  danger: "#ff3b30"
  danger-light: "#fff1f2"
  info: "#3b82f6"
  info-light: "#eff6ff"
  highlight: "#fff7ed"
  highlight-hover: "#ffedd5"
typography:
  body:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'Microsoft YaHei', system-ui, 'PingFang SC', 'Segoe UI', 'Noto Sans CJK SC', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif"
    fontSize: 14px
    fontWeight: 400
    lineHeight: 20px
    letterSpacing: 0
  body-sm:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'Microsoft YaHei', system-ui, 'PingFang SC', 'Segoe UI', 'Noto Sans CJK SC', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif"
    fontSize: 13px
    fontWeight: 400
    lineHeight: 20px
    letterSpacing: 0
  caption:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'Microsoft YaHei', system-ui, 'PingFang SC', 'Segoe UI', 'Noto Sans CJK SC', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif"
    fontSize: 12px
    fontWeight: 400
    lineHeight: 16px
    letterSpacing: 0
  title:
    fontFamily: "-apple-system, BlinkMacSystemFont, 'Microsoft YaHei', system-ui, 'PingFang SC', 'Segoe UI', 'Noto Sans CJK SC', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif"
    fontSize: 16px
    fontWeight: 600
    lineHeight: 24px
    letterSpacing: 0
spacing:
  none: 0
  xxs: 2px
  xs: 4px
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  xxl: 32px
  section: 40px
rounded:
  none: 0
  sm: 2px
  md: 4px
  lg: 8px
  full: 999px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.text-inverse}"
    rounded: "{rounded.md}"
    typography: "{typography.caption}"
    height: 28px
    padding: 4px 12px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.text-inverse}"
    rounded: "{rounded.md}"
  button-primary-pressed:
    backgroundColor: "{colors.primary-pressed}"
    textColor: "{colors.text-inverse}"
    rounded: "{rounded.md}"
  button-primary-disabled:
    backgroundColor: "{colors.primary-disabled}"
    textColor: "{colors.text-inverse}"
    rounded: "{rounded.md}"
  button-default:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-secondary}"
    rounded: "{rounded.md}"
    typography: "{typography.caption}"
    height: 28px
    padding: 4px 12px
  input:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-primary}"
    rounded: "{rounded.md}"
    typography: "{typography.body-sm}"
    height: 28px
    padding: 4px 8px
  input-focus:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-primary}"
    rounded: "{rounded.md}"
  input-disabled:
    backgroundColor: "{colors.background-muted}"
    textColor: "{colors.text-disabled}"
    rounded: "{rounded.md}"
  table-header:
    backgroundColor: "{colors.border-light}"
    textColor: "{colors.text-primary}"
    typography: "{typography.body-sm}"
    height: 30px
  table-row:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-primary}"
    typography: "{typography.body-sm}"
    height: 35px
  table-row-selected:
    backgroundColor: "{colors.background-selected}"
    textColor: "{colors.text-primary}"
  card:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-primary}"
    rounded: "{rounded.md}"
    padding: 16px
  modal:
    backgroundColor: "{colors.background}"
    textColor: "{colors.text-primary}"
    rounded: "{rounded.lg}"
  tag-success:
    backgroundColor: "{colors.success-light}"
    textColor: "{colors.success}"
    rounded: "{rounded.md}"
  tag-warning:
    backgroundColor: "{colors.warning-light}"
    textColor: "{colors.warning}"
    rounded: "{rounded.md}"
  tag-danger:
    backgroundColor: "{colors.danger-light}"
    textColor: "{colors.danger}"
    rounded: "{rounded.md}"
---

# Tinper Web Enterprise

## Overview

Tinper Web Enterprise 是面向 TinperNext（`@tinper/next-ui`）与 TinperNextPro（`tne-tinpernextpro-fe`）的企业级 Web 设计系统。它服务于高密度业务页面，重点覆盖查询表单、数据表格、可编辑表格、参照选择、抽屉、弹窗、卡片、标签页和工作台布局。

界面应保持清晰、紧凑、业务导向。优先保证信息组织效率，不做装饰性构图。实现 CSS 变量时，以 `designtoken.css` 中的 token 值为来源。

## Colors

主品牌色是红色（`#e60012`）。只用于主操作、选中态、品牌强调和激活导航。悬停态和按下态使用更深的品牌色阶。

界面主体由中性灰承载。文本使用 `text-primary`、`text-secondary` 和 `text-tertiary`；禁用文本和占位文本使用 `text-disabled`。默认背景为白色，弱背景使用接近白色的灰，表格选中行使用蓝色选中背景。

语义色只表达状态含义：成功、警告、危险和信息。浅色变体用于标签和提示背景，基础色用于图标、文本和边框。

## Brand Override Strategy

当设计图主视觉色与当前默认品牌色不一致时：

- 若该视觉只服务于单页活动或临时页面，可保留局部视觉覆盖
- 若该视觉服务于当前 app 的正式首页或稳定业务域，应优先覆盖品牌 token，而不是在页面中重复定义颜色变量

推荐优先覆盖的 token：

- `--brand-50` ~ `--brand-900`
- 品牌相关全局主色 token（例如主按钮、品牌文字、选中态、激活态所依赖的 token）
- 选中态、品牌边框、品牌图标所依赖的全局 token

<!-- 默认不应改写的 token：

- `success` 语义 token
- `warning` 语义 token
- `danger` 语义 token

如果页面主要品牌色仍依赖页面私有 token 或散落的 hex 值，而不是依赖上述品牌 token，则说明主题覆盖方案尚未完成。 -->

## Typography

使用 `--fm` 定义的中文企业级系统字体栈。页面基础正文为 14px，高密度组件文本为 13px，紧凑标签和按钮文本为 12px。表格和表单的行高应保持实用：正文和输入文本使用 20px，辅助说明使用 16px。

标题、选中标签页、重要标签和语义标签使用 600 字重。正文、表格、表单和导航中的大多数文本保持 400 字重。

## Layout

使用以 4px 为基础的紧凑间距体系，常用组件间距为 8px 和 12px。表单和表格应保持稳定的纵向节奏：输入框和按钮高度为 28px，表头高度为 30px，表格行高为 35px。

查询表单使用弱化的 `background-searchform` 背景。数据页面优先保证扫描效率：查询区在前，操作工具栏其次，表格主体随后，分页或汇总信息最后。

## Elevation & Depth

系统整体以扁平风格为主。默认使用边框和背景层级表达视觉层次。阴影只用于弹窗、抽屉、气泡卡片、工具提示、通知、消息和浮层选择面板。

普通页面区域、查询表单、表格和卡片不要额外添加阴影，除非现有 Tinper 组件已经内置该效果。

## Shapes

普通控件和容器使用 4px 圆角。弹窗、抽屉、气泡卡片、气泡确认、工具提示、通知和消息等反馈类浮层使用 8px 圆角。小型复选框或紧凑标记使用 2px 圆角。全圆角只用于胶囊、开关、徽标、锚点和圆形拖拽柄。

## Components

主按钮使用品牌红背景和白色文字。默认按钮使用白色背景、次级文本和中性边框。禁用控件使用弱化灰色背景和禁用文本色。

输入框使用 28px 高度、13px 文本、白色背景和 4px 圆角。聚焦态使用蓝色焦点边框。必填或错误输入框使用 `designtoken.css` 中的警告或危险语义 token。

表格使用紧凑密度：30px 表头、35px 行高、13px 文本、浅灰表头背景和中性边框。选中行使用蓝色选中背景；搜索命中、 subtotal 和 total 行使用高亮背景。

卡片、弹窗、抽屉和反馈浮层使用白色背景，并使用语义化标题和内容文本 token。标签页在选中或激活时使用主色，默认状态使用中性文本色。

## Do's and Don'ts

优先使用 TinperNext 和 TinperNextPro 的组件能力，再编写自定义视觉规则。

企业级页面应保持紧凑、规整、易扫描。

使用 primary、danger、warning、selected、disabled、background 等语义 token，不直接硬编码 CSS 值。

保留 `designtoken.css` 作为 CSS 自定义属性的实现来源。

业务操作页面不要构建营销式首屏、过大的装饰卡片或依赖插画的布局。

不要把主红色用于大面积背景、普通正文或非操作装饰。

不要引入 token 集合之外的任意圆角、阴影或字号。

不要重命名现有 `--ynfw-*` 或 `--wui-*` CSS 变量，除非同步更新实现来源文件。
