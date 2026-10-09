# 布局使用模式（来自真实项目蒸馏）

## 0. NextPro Layouts 页面骨架

NextPro 页面布局组件从 `tne-tinpernextpro-fe/layouts` 导入，详细 API 见 `../references/layouts/README.md`。

```tsx
import {
  DetailLayout,
  LineTabs,
  ListLayout,
  ToolbarLayout,
  TreeTableLayout,
} from 'tne-tinpernextpro-fe/layouts';
```

| 场景 | 组件 | 文档 |
| --- | --- | --- |
| 列表页查询区 + 工具栏 + 表格 | `ListLayout` | `../references/layouts/ListLayout.md` |
| 详情页头部 + 表单 + 底部操作 | `DetailLayout` | `../references/layouts/DetailLayout.md` |
| 详情页子表/分组页签 | `LineTabs` | `../references/layouts/LineTabs.md` |
| 按钮工具栏对齐 | `ToolbarLayout` | `../references/layouts/ToolbarLayout.md` |
| 左树右表 / 左树右卡片 | `TreeTableLayout` | `../references/layouts/TreeTableLayout.md` |

### 列表页骨架

```tsx
<ListLayout>
  <SearchForm ref={searchRef} onSearch={reload} onReset={reload} />
  <ToolbarLayout>
    <Button colors="primary" onClick={handleCreate}>新增</Button>
  </ToolbarLayout>
  <DataGrid rowKey="id" data={rows} columnDefs={columns} pagination={pagination} />
</ListLayout>
```

### 详情页骨架

```tsx
<DetailLayout>
  <DetailLayout.Header>
    <h2>单据详情</h2>
  </DetailLayout.Header>
  <DataForm ref={formRef} formMode={formMode} />
  <LineTabs items={tabItems} />
  <DetailLayout.Footer>
    <ToolbarLayout>
      <Button onClick={handleCancel}>取消</Button>
      <Button colors="primary" onClick={handleSave}>保存</Button>
    </ToolbarLayout>
  </DetailLayout.Footer>
</DetailLayout>
```

## 1. Layout.Spliter 可拖拽侧边栏

真实项目中用于主面板+详情面板的左右分栏：

```jsx
import { Layout } from '@tinper/next-ui';
const { Sider, Content, Spliter } = Layout;

<Layout style={{ height: '100%' }}>
  <Sider width={280} style={{ background: '#fff' }}>
    <Tree treeData={menuData} onSelect={handleSelect} />
  </Sider>
  <Spliter />
  <Content style={{ padding: 16 }}>
    <DataTable columns={columns} request={fetchData} />
  </Content>
</Layout>
```

## 2. 栅格布局（Row + Col）

```jsx
<Row gutter={16}>
  <Col span={8}><Card title="统计1">...</Card></Col>
  <Col span={8}><Card title="统计2">...</Card></Col>
  <Col span={8}><Card title="统计3">...</Card></Col>
</Row>
```

响应式：`<Col xs={24} sm={12} md={8} lg={6} xl={4}>`

## 3. Space 工具栏模式

几乎所有操作栏都用 Space 包裹：

```jsx
<Space>
  <Button type="primary" onClick={handleAdd}>新增</Button>
  <Button onClick={handleBatchDelete} disabled={!selectedKeys.length}>批量删除</Button>
  <Dropdown.Button overlay={moreMenu}>更多操作</Dropdown.Button>
  <Tooltip overlay="刷新"><Button onClick={handleRefresh}><Icon type="uf-refresh" /></Button></Tooltip>
</Space>
```

## 4. Tabs + 内容区域

```jsx
<Tabs activeKey={activeKey} onChange={setActiveKey} type="line">
  <Tabs.TabPane tab="基本信息" key="basic">
    <DataForm ref={basicFormRef} formMode="browse" />
  </Tabs.TabPane>
  <Tabs.TabPane tab="订单明细" key="detail">
    <EditTable ref={detailTableRef} columns={detailColumns} />
  </Tabs.TabPane>
  <Tabs.TabPane tab="操作日志" key="log">
    <DataTable columns={logColumns} request={fetchLogs} />
  </Tabs.TabPane>
</Tabs>
```

## 5. Collapse 折叠面板 + 表单

```jsx
<Collapse defaultActiveKey={['basic']}>
  <Collapse.Panel header="基本信息" key="basic">
    <DataForm ref={basicRef} formLayout={3}>
      <DataForm.Item label="名称" name="name" inputType="input" required />
      <DataForm.Item label="编码" name="code" inputType="input" required />
    </DataForm>
  </Collapse.Panel>
  <Collapse.Panel header="扩展信息" key="extra">
    <DataForm ref={extraRef} formLayout={3}>
      <DataForm.Item label="备注" name="remark" inputType="textarea" colSpan={24} />
    </DataForm>
  </Collapse.Panel>
</Collapse>
```

## 6. Upload.Dragger 拖拽上传

```jsx
<Upload.Dragger
  action="/api/upload"
  accept=".xlsx,.csv"
  fileList={fileList}
  onChange={({ fileList }) => setFileList(fileList)}
  beforeUpload={(file) => {
    const isLt10M = file.size / 1024 / 1024 < 10;
    if (!isLt10M) Message.error('文件不能超过 10MB');
    return isLt10M;
  }}
>
  <p><Icon type="uf-cloud-o-up" style={{ fontSize: 48 }} /></p>
  <p>点击或拖拽文件到此区域上传</p>
</Upload.Dragger>
```

## 7. Spin 加载遮罩（三种模式）

### 组件级遮罩（最高频，不包裹子节点）

```jsx
<div style={{ position: 'relative' }}>
  <Spin getPopupContainer={this} spinning={loading} tip="加载中..." />
  {/* 内容区域 */}
</div>
```

`getPopupContainer={this}` 让 Spin 作为兄弟节点覆盖在容器上，不需要包裹子节点。

### 路由懒加载 fallback

```jsx
<Suspense fallback={<Spin spinning />}>
  <Routes />
</Suspense>
```

### 全屏加载

```jsx
<Spin fullScreen showBackDrop spinning={loading} />
```

## 8. Message 防重复 + 真实颜色值

真实项目中用 `Message.create()` + `Message.destroy()` 防止重复弹出：

```js
Message.destroy();
Message.create({ content: '操作成功', color: 'successlight', duration: 3 });
```

**完整颜色值**（源码 + 真实项目验证）：
- 标准：`success` / `info` / `warning` / `danger` / `dark` / `light`
- Light 系列（真实项目高频使用）：`successlight` / `infolight` / `warninglight` / `dangerlight`
- `Message.error()` 内部映射为 `danger` 颜色

## 9. ErrorMessage 先 destroy 再 create

ErrorMessage 不会自动关闭前一个实例，需要先手动销毁：

```js
ErrorMessage.destroy();
ErrorMessage.create({
  message: errorContent,
  isCopy: false,
  uploadable: 0,
  footer: (defaultFooter) => (
    <Button onClick={() => ErrorMessage.destroy()}>关闭</Button>
  ),
});
```

## 10. Upload customRequest 完全接管上传

真实项目中不用 `action` URL，而用 `customRequest` 手动控制上传流程：

```jsx
<Upload
  multiple={false}
  fileList={fileList}
  customRequest={({ file }) => {
    if (file.size > 10 * 1024 * 1024) {
      Message.error('文件不能超过 10MB');
      return;
    }
    setFileList([{ uid: '1', name: file.name, status: 'done' }]);
    setFile(file);
  }}
  onRemove={() => { setFileList([]); setFile(null); }}
>
  <Button><Icon type="uf-upload" /> 点击上传</Button>
</Upload>
```
