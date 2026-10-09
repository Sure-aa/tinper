# Modal 使用模式（来自真实项目蒸馏）

> 来源：安装器（~77 处）、云管理套件（~83 处），共 ~160 个文件中的 Modal 使用。

## 1. 声明式 vs 命令式选择

| 场景 | 选择 | 说明 |
|------|------|------|
| 自定义复杂内容（表单/表格/多步操作） | 声明式 `<Modal visible={}>` | 需要内部组件状态或 ref |
| 删除确认、简单提示 | `Modal.confirm()` | 一行搞定 |
| 操作结果反馈（批量成功/失败） | `Modal.success()` / `Modal.error()` | 带自定义 footer |
| 需要弹窗外动态更新内容 | `Modal.confirm()` + `modal.update()` | 保存引用后更新 |

## 2. 命令式弹窗的高级用法

### 保存引用 + 手动 destroy

```js
const modal = Modal.confirm({
  title: '确定删除吗?',
  getPopupContainer: (dom) => dom,  // 微前端项目必加
  onOk: async () => {
    await deleteItem(id);
    modal.destroy();
  },
});
```

> **微前端必须项**：命令式弹窗（`Modal.confirm/info/success/error/warning`）默认挂载到 `document.body`，在微前端沙箱中会逃逸。必须传 `getPopupContainer: (dom) => dom` 将弹窗挂载到当前应用容器内。

### update 更新已打开弹窗的内容

```js
showRestartModal() {
  const props = {
    title: '重启',
    content: (<div><Switch onChange={() => this.showRestartModal()} /><p>确定要重启吗？</p></div>),
    onOk: () => { this.onRestart(); this.modal.destroy(); this.modal = null; },
    onCancel: () => { this.modal.destroy(); this.modal = null; },
  };
  if (this.modal) {
    this.modal.update(props);
  } else {
    this.modal = Modal.confirm(props);
  }
}
```

### Modal.destroyAll() 关闭所有弹窗

```js
Modal.destroyAll();
```

### 批量操作结果三态反馈

```js
if (failSize === 0) {
  const modal = Modal.success({
    title: '执行成功',
    content: <span>共执行 {totalSize} 条，成功 {successSize} 条</span>,
    footer: <Button colors="primary" onClick={() => modal.destroy()}>知道了</Button>,
  });
} else if (successSize === 0) {
  const modal = Modal.error({ title: '全部执行失败', content: ..., footer: ... });
} else {
  const modal = Modal.warning({ title: '部分执行失败', content: ..., footer: ... });
}
```

## 3. Modal 嵌套组件的 7 种组合

### Modal + DataForm（推荐，新项目）
```jsx
<Modal title="新增基线" visible={visible} onOk={handleOk} onCancel={close}
       maskClosable={false}>
  <DataForm ref={formRef} formLayout={2}>
    <DataForm.Item label="名称" name="name" inputType="input" required />
    <DataForm.Item label="描述" name="desc" inputType="textarea" />
  </DataForm>
</Modal>
```

### Modal + Form（旧项目 HOC 式）
```jsx
<Modal visible={visible} width={600}>
  <Modal.Header closeButton><Modal.Title>添加数据中心</Modal.Title></Modal.Header>
  <Modal.Body>
    <Form labelCol={{ span: 5 }} wrapperCol={{ span: 17 }}>
      <Form.Item label="名称" rules={[{ required: true }]}>
        <Input {...getFieldProps('name', { rules: [...] })} />
      </Form.Item>
    </Form>
  </Modal.Body>
  <Modal.Footer>
    <Button onClick={close}>取消</Button>
    <Button colors="primary" onClick={handleSubmit}>确定</Button>
  </Modal.Footer>
</Modal>
// export default Form.createForm()(AddModal)
```

### Modal + DataTable（用户搜索/选择）
弹窗中展示 DataTable 并支持勾选。

### Modal + EditTable（可编辑表格弹窗）
弹窗内嵌入 EditTable，常见于规则配置场景。

### Modal + Tabs（日志/分类查看）
弹窗内用 Tabs 区分不同类别内容。

### Modal + DataForm + Collapse（授权场景）
弹窗内用 Collapse 组织多个表单区域。

### Modal 作为全屏容器
```jsx
<Modal visible={visible} mask={false} header={null} footer={null} isMaximize>
  <Modal.Body><DataTable fillSpace {...props} /></Modal.Body>
</Modal>
```

## 4. 关闭保护模式（cancelConfirm）

真实项目封装了关闭保护：点击关闭/取消时弹出二次确认。

**实现思路**（不建议直接封装 Wrapper，用工具函数）：
```js
function confirmBeforeClose(onCancel) {
  return () => new Promise((resolve) => {
    Modal.confirm({
      title: '确定退出此页面吗？若有未保存数据将丢失',
      onOk: () => { onCancel?.(); resolve(true); },
      onCancel: () => { resolve(false); },
    });
  });
}

// 使用
<Modal onCancel={confirmBeforeClose(() => setVisible(false))} />
```

## 5. 常用 props 配置速查

| prop | 典型值 | 说明 |
|------|--------|------|
| `width` | `600`（表单）/ `800`（中型）/ `1200`（大表格）/ `"80%"` / `"90%"`（日志） | 按内容决定 |
| `destroyOnClose` | `true`（默认值） | 默认已开启，无需显式传；若需保留弹窗状态可设 `false` |
| `maskClosable` | `false`（默认值） | 默认已禁止点蒙层关闭，表单弹窗无需额外设置；信息弹窗可设 `true` |
| `getPopupContainer={(dom) => dom}` | 微前端项目必加 | 防止弹窗挂载到 body 导致沙箱逃逸 |
| `okButtonProps={{ loading }}` | `{ loading: submitting }` | 确认按钮加载态 |
| `okButtonProps={{ disabled }}` | `{ disabled: !selectedRowKeys.length }` | 确认按钮禁用态 |
| `cancelButtonProps={{ style: { display: 'none' } }}` | — | 隐藏取消按钮（只读弹窗） |
| `footerProps.onCustomRender` | `(children) => [<Button>测试连接</Button>, children]` | 在默认按钮前插入自定义按钮 |
| `bodyStyle={{ padding: 0 }}` | — | 让内容组件自管间距 |
| `isMaximize` | `true` | 以最大化状态打开 |
| `draggable` | `true` | 可拖拽（命令式弹窗默认不可拖拽） |
