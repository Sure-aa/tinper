# 组件使用模式（来自真实项目蒸馏）

## 1. Alert 提示条

### type vs colors 优先级

Alert 同时接受 `type` 和 `colors` 两个属性，`type` 优先。`type` 支持 `"error"` 并自动映射为 `"danger"`，`colors` 不接受 `"error"`：

```jsx
// ✅ 推荐 — 用 type，可以写 error
<Alert type="warning" closable={false}>拆分期间将会中断服务</Alert>
<Alert type="error" closable={false}>存在异常的产品盘</Alert>

// ✅ 也可以 — 用 colors
<Alert colors="danger" showIcon closable={false}>检查失败</Alert>
<Alert colors="success" closeLabel="">安装完成</Alert>
```

**colors 取值**: `success` / `info` / `warning` / `danger`（默认 `warning`）
**type 取值**: `success` / `info` / `warning` / `danger` / `error`（error → danger）

### closable 默认 true，但真实项目几乎都关闭

源码默认 `closable={true}`，但真实项目 17 处使用中 15 处显式传 `closable={false}`。提示条场景下通常不允许用户关闭：

```jsx
// 表单/弹窗内的上下文提示（最高频）
<Alert type="info" closable={false}>待处理数为0时才能同步</Alert>

// Modal.Body 内的警告横幅
<Modal.Body>
  <Alert type="warning" closable={false} style={{ marginBottom: 20 }}>
    此操作不可逆，请确认后执行
  </Alert>
  <Form>{/* ... */}</Form>
</Modal.Body>
```

### closeLabel="" 隐藏关闭按钮的替代方案

真实项目中也用 `closeLabel=""` 替代 `closable={false}` 来隐藏关闭按钮：

```jsx
<Alert colors="success" closeLabel="">
  <span className="result-title">安装完成</span>
  <Button onClick={onAck} bordered>知道了</Button>
</Alert>
```

---

## 2. Tag 状态标签（Table 列渲染高频模式）

### 颜色值分三档

| 分类 | 值 | 效果 |
|------|---|------|
| 语义色 | `success` `warning` `danger` `info` `invalid` `start` | 纯色背景 |
| 半透明色 | `half-blue` `half-green` `half-red` `half-yellow` `half-dark` | 25% 透明背景 + 深色文字 |
| 预设色 | `purple` `green` `orange` `pink` | 边框色卡 |

任意字符串（如 `"#DC2626"`）会作为自定义背景色。

### Table 列状态映射模式（最高频用法）

```jsx
const STATUS_MAP = {
  0: { color: 'half-yellow', name: '待安装' },
  1: { color: 'half-blue',   name: '安装中' },
  2: { color: 'half-red',    name: '安装失败' },
  3: { color: 'half-green',  name: '安装成功' },
};

const columns = [{
  title: '状态',
  dataIndex: 'status',
  render: (text) => (
    <Tag color={STATUS_MAP[text]?.color}>{STATUS_MAP[text]?.name}</Tag>
  ),
}];
```

语义色在审批/流水线场景：

```jsx
const APPROVE_COLOR = {
  TO_APPROVE: 'info',
  APPROVED: 'success',
  REJECTED: 'danger',
};

render: (text) => <Tag size="sm" color={APPROVE_COLOR[text]}>{text}</Tag>
```

**注意**: Table 内的 Tag 建议加 `size="sm"` 保持紧凑。

---

## 3. Popconfirm 气泡确认

### 确认回调是 onClose，不是 onConfirm

`onConfirm` 已废弃，源码中 `onConfirm` 存在但优先级低于 `onClose`。新代码统一用 `onClose`：

```jsx
// ✅ 正确
<Popconfirm
  content="确定删除该记录吗？"
  onClose={handleDelete}
  onCancel={() => {}}
>
  <Button>删除</Button>
</Popconfirm>

// ❌ 废弃写法
<Popconfirm onConfirm={handleDelete}>...</Popconfirm>
```

### content vs title vs description

| 属性 | 用途 |
|------|------|
| `content` | 确认消息主体（推荐） |
| `description` | `content` 的别名，两者渲染同一位置，`content` 优先 |
| `title` | 标题区域（位于 content 上方，可选） |

```jsx
<Popconfirm
  title="删除确认"
  content="此操作不可逆，确定要删除吗？"
  onClose={handleDelete}
/>
```

### 其他实用属性

| 属性 | 默认值 | 说明 |
|------|--------|------|
| `placement` | `'top'` | 弹出方向 |
| `okText` / `cancelText` | 国际化 | 自定义按钮文案 |
| `okButtonProps` / `cancelButtonProps` | — | 按钮 props 透传 |
| `showCancel` | `true` | 是否显示取消按钮 |
| `disabled` | `false` | 禁用弹出 |
| `keyboard` | `false` | 启用键盘快捷键（Alt+Y/N, Esc） |
| `close_btn` / `cancel_btn` | — | 完全自定义按钮元素 |

---

## 4. Steps 步骤条

### direction="vertical" 是主流用法

真实项目 8 处 Steps 使用中 7 处为 `direction="vertical"`，水平步骤条只用于顶部向导导航。

### 三种模式

**模式 A — 顶部向导（水平）**：
```jsx
<Steps current={currentStep}>
  <Step title="安装规划" />
  <Step title="配置预览与检查" />
</Steps>
{currentStep === 0 ? <PlanForm /> : <PreviewCheck />}
```

**模式 B — Modal 内多步表单（垂直 + description 承载表单）**：
```jsx
<Steps direction="vertical" current={currentStep} type="number">
  <Step title="数据中心信息" description={
    <Form>{/* 第一步表单内容 */}</Form>
  } />
  <Step title="环境信息" description={
    <Select>{/* 第二步选择内容 */}</Select>
  } />
</Steps>
```

**模式 C — 日志/进度追踪（垂直 + 动态 status/icon）**：
```jsx
const STATUS_MAP = {
  Installing: 'process',
  Success: 'finish',
  Failed: 'error',
  '': 'wait',
};

<Steps direction="vertical" current={0}>
  {taskItems.map(item => (
    <Step
      status={STATUS_MAP[item.status]}
      icon={item.status === 'Installing' ? <Icon type="uf-loadingstate" /> :
            item.status === '' ? <Icon type="uf-sync-c-o" style={{ color: '#ccc' }} /> : null}
      title={<span onClick={() => jumpTo(item)}>{item.name}</span>}
      description={/* 子任务列表 */}
    />
  ))}
</Steps>
```

---

## 5. Drawer 抽屉

### 宽度约定

| 场景 | 宽度 | 说明 |
|------|------|------|
| 中型详情面板 | `720`–`740` | 健康信息、JSON 查看器 |
| 大型表格/详情 | `900`–`1100` | 产品列表、表格+操作 |
| 自适应 | `'50%'` | 响应式面板 |

### 在 Modal 上方弹出时必须设 zIndex

Drawer 在 Modal 之上弹出时，需显式设置 `zIndex` 确保层级正确：

```jsx
<Drawer visible={visible} width={900} zIndex={1200}>
  <Tabs>
    <Tabs.TabPane tab="详情" key="detail">...</Tabs.TabPane>
    <Tabs.TabPane tab="日志" key="log">...</Tabs.TabPane>
  </Tabs>
</Drawer>
```

### Drawer.Footer 表单提交模式

```jsx
<Drawer visible={visible} width="50%" showMask showClose maskClosable={false}>
  <Form ref={formRef}>{/* 表单内容 */}</Form>
  <Drawer.Footer>
    <Button onClick={onCancel}>取消</Button>
    <Button colors="primary" onClick={handleSubmit}>确定</Button>
  </Drawer.Footer>
</Drawer>
```

### 微前端容器内 Drawer

```jsx
<Drawer
  visible={visible}
  width={740}
  zIndex={1900}
  style={{ position: 'absolute' }}
  getPopupContainer={containerRef.current}
  mask
  maskClosable
/>
```

---

## 6. Collapse 折叠面板

### Panel 可脱离 Collapse 独立使用

源码中 `Collapse.Panel` 支持独立使用，作为可展开/收起的容器：

```jsx
const { Panel } = Collapse;

<Panel collapsible expanded={!isCollapsed} onClick={toggleCollapse}>
  {children}
</Panel>
```

### 嵌套 Collapse 模式（配置管理场景）

```jsx
<Collapse defaultActiveKey={appKeys} ghost={false} type="card">
  {apps.map(app => (
    <Collapse.Panel header={app.name} key={app.id} showArrow>
      <Collapse defaultActiveKey={['config', 'db']} ghost={false} type="card">
        <Collapse.Panel header="微服务配置" key="config">...</Collapse.Panel>
        <Collapse.Panel header="数据库配置" key="db">...</Collapse.Panel>
      </Collapse>
    </Collapse.Panel>
  ))}
</Collapse>
```

### 常用 type 值

| type | 场景 |
|------|------|
| `"card"` | 有边框卡片式，配合 `ghost={false}` |
| `"list"` | 简洁列表式 |
| 不设（默认） | 标准手风琴 |

### 全部展开 + 自定义展开图标

```jsx
<Collapse
  defaultActiveKey={['1','2','3','4']}
  expandIcon={({ isActive }) => <img src={isActive ? openIcon : closeIcon} />}
>
```

---

## 7. Badge 徽标数

### count={null} 隐藏徽标

`count={null}` 完全隐藏徽标（不渲染），区别于 `count={0}`（默认也隐藏，除非 `showZero`）：

```jsx
// 有上下文时显示数量，无上下文时隐藏
<Badge count={!dcName ? null : totalTask}>
  <Button>安装任务</Button>
</Badge>
```

### Badge 包裹 Button（最高频模式）

```jsx
<Badge count={pendingCount} style={{ marginRight: 10 }}>
  <Button type="link" onClick={openTaskList}>安装任务</Button>
</Badge>
```

### Badge 在 TabPane 标题中

```jsx
<Tabs>
  <Tabs.TabPane tab={<Badge count={objectTotal}>对象存储审批</Badge>} key="1">
    ...
  </Tabs.TabPane>
  <Tabs.TabPane tab={<Badge count={domainTotal}>域名审批</Badge>} key="2">
    ...
  </Tabs.TabPane>
</Tabs>
```

### showZero + overflowCount

```jsx
<Badge colors="primary" showZero overflowCount={9} count={typeCount} />
```
