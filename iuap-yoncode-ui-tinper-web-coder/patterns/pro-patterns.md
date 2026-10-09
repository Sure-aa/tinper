# Pro 组件使用模式（来自真实项目蒸馏）

> NextPro 支撑服务（审批、草稿、打印、上传、自动编码、MDF 参照/过滤）的组合模式见 `./support-patterns.md`。

## 1. DataTable ref 方法

真实项目中 DataTable ref 几乎只用 `reload()`，其他查询方法很少调用：

### reload() — 刷新数据（最高频）

```jsx
const tableRef = useRef();

// 基本刷新（CRUD 操作后、搜索条件变化后）
tableRef.current?.reload();

// 指定页码刷新（删除后跳转到指定页）
tableRef.current?.reload(pageNum);

<DataTable ref={tableRef} columns={columns} request={fetchData} />
```

### 常用 ref 方法速查

| 方法 | 说明 | 真实调用频率 |
|------|------|------------|
| `reload([pageNum])` | 刷新数据，可指定页码 | 极高（20+ 处） |
| `getSelectedRowKeys()` | 获取选中行 keys | 中（删除前获取选中） |
| `getSelectedRowData()` | 获取选中行完整数据 | 中 |
| `clearSelectedRowKeys()` | 清除选中 | 中（操作后清除） |
| `getDataSource()` | 获取当前数据 | 低 |

---

## 2. SearchForm submitter 三种模式

### 模式 A — 在默认按钮旁添加额外按钮（最常用）

```jsx
<SearchForm
  ref={searchRef}
  formLayout={4}
  onSearch={(values) => tableRef.current?.reload()}
  onReset={() => tableRef.current?.reload()}
  submitter={{
    render(props, dom) {
      return [...dom, <Button onClick={handleRefresh}>刷新</Button>];
    },
  }}
>
  <SearchForm.Item label="名称" name="name" inputType="input" />
</SearchForm>
```

> **注意**: `onSearch` / `onReset` 直接放在 SearchForm props 上，submitter 只用于渲染定制。

### 模式 B — 完全替换按钮区域

```jsx
<SearchForm submitter={{ render(props, dom) { return [customBtn]; } }}>
```

### 模式 C — 隐藏按钮区域

```jsx
<SearchForm submitter={false}>
```

### hiddenKeys 动态隐藏字段

```jsx
<SearchForm hiddenKeys={isPrivateEnv ? ['type', 'name'] : undefined}>
  <SearchForm.Item label="类型" name="type" inputType="select" />
  <SearchForm.Item label="名称" name="name" inputType="input" />
</SearchForm>
```

### ref 方法

```jsx
searchFormRef.current.setFieldsValue({ name: externalValue });
```

---

## 3. DataForm formMode 切换

三种模式值：`'edit'`（可编辑）、`'browse'`（只读）、`'add'`（新增，行为等同 edit）。

### 动态切换模式（最常用）

模式通过父组件 state 控制，不在 DataForm 内部切换：

```jsx
const formMode = pageType === 'view' ? 'browse' : 'edit';

<DataForm ref={formRef} formMode={formMode} formLayout={2}>
  <DataForm.Item label="名称" name="name" inputType="input" required />
  <DataForm.Item label="编码" name="code" inputType="input" required />
</DataForm>
```

### 静态浏览模式

```jsx
<DataForm formMode="browse" disabledKeys={[]}>
  <DataForm.Item label="审计对象" name="objectName" inputType="input" />
  <DataForm.Item label="操作类型" name="operType" inputType="select" />
</DataForm>
```

> `disabledKeys={[]}` 常与 `formMode='browse'` 搭配，确保无字段被意外禁用。

---

## 4. EditTable 行内编辑

### 完整配置示例

```jsx
const editTableRef = useRef();

<EditTable
  fillSpace
  rowKey="id"
  type="inlineForm"
  autoEditedByClickRows={false}
  ref={editTableRef}
  data={mainData}
  columns={[
    {
      title: '逻辑编码', dataIndex: 'logicCode',
      editType: 'select',
      editOptions: { options: logicCodes },
      required: true,
      onCellChange: (record, column, value) => {
        editTableRef.current.saveMultiCellData({
          rowData: { ...record, schemaName: defaultSchema },
          callback: (newData) => setMainData(newData),
        });
      },
    },
    {
      title: '表名', dataIndex: 'tableName',
      editType: 'input',
      required: true,
    },
    {
      title: '加密策略', dataIndex: 'strategyCode',
      editType: 'select',
      editOptions: { options: strategyOptions },
      required: true,
    },
    {
      title: '策略名称', dataIndex: 'strategyName',
      editType: 'input',
      editAbled: (record) => record.strategyCode === 'MF0',
    },
    {
      title: '状态', dataIndex: 'enableStatus',
      editAbled: false,
    },
  ]}
  rowSelection={{ type: 'checkbox', selectedRowKeys, onChange: onChangeSelected }}
  pagination
  operationItems={(record) => [...]}
  operationClick={operationClick}
/>
```

### EditTable ref 方法（真实使用频率）

| 方法 | 参数 | 说明 |
|------|------|------|
| `addRow({ rowData, callback })` | `rowData`: 数组 | 添加行 |
| `addRowAfter({ posRowKey, rowData })` | `posRowKey`: 指定位置 | 在某行后插入 |
| `editRow({ rowKey, edit, callback })` | `edit`: boolean | 切换行编辑状态 |
| `saveMultiCellData({ rowData, callback })` | `rowData`: 修改数据 | 保存单元格数据 |
| `cancel({ rowKey })` | — | 取消行编辑 |
| `deleteData({ rowKey })` | — | 删除行 |
| `validate({ callback })` | `callback(errors)` | 校验所有编辑行 |
| `getAllData()` | — | 获取全部数据 |

### editAbled 条件编辑

```jsx
{
  dataIndex: 'name',
  editType: 'input',
  editAbled: (record) => record.status !== '0',  // 函数：按行数据决定
}

{
  dataIndex: 'status',
  editAbled: false,  // boolean：整列不可编辑
}
```

---

## 5. DataGrid ref 方法

```jsx
const tableRef = useRef();
// DataGrid 是 data 驱动，不做异步请求；服务端分页由调用方自行请求后回填 data
<DataGrid ref={tableRef} columnDefs={columnDefs} data={data} />
```

### 常用 ref 方法速查

| 方法 | 说明 | 使用场景 |
|------|------|---------|
| `reload()` | 用当前 `data` 重刷内部 state（**不发请求**） | 调用方回填 `data` 后刷新 |
| `getSelectedRowKeys()` | 获取已选行 key | 批量操作前 |
| `getSelectedRows()` | 获取已选行数据 | 批量操作前 |
| `clearSelection()` | 清空选择 | 操作完成后 |
| `getData()` | 获取当前数据 | 低频 |

> DataGrid 是 `data` 驱动，无 `query/reset`；服务端分页由调用方在 `pagination.onChange` 自取后回填 `data`。

---

## 6. EditGrid 行内编辑

### 完整配置示例

```jsx
const editRef = useRef();

<EditGrid
  ref={editRef}
  rowKey="id"
  data={data}
  editTrigger="click"
  columnDefs={[
    {
      field: 'name',
      headerName: '名称',
      width: 180,
      editable: true,
      editor: 'input',
      rules: [{ required: true, message: '名称不能为空' }],
    },
    {
      field: 'type',
      headerName: '类型',
      width: 140,
      editable: true,
      editor: 'select',
      editorProps: { options: typeOptions },
    },
    {
      field: 'qty',
      headerName: '数量',
      width: 100,
      editable: true,
      editor: 'number',
      editorProps: { min: 1, precision: 0 },
      rules: [{ validator: v => v > 0 ? undefined : '数量必须大于 0' }],
    },
    {
      field: 'status',
      headerName: '状态',
      editable: (record) => record.type !== 'locked', // 按行条件决定是否可编辑
      editor: 'switch',
    },
  ]}
  showRowNum={{ width: 58, pinned: 'left' }}
  rowSelection={{ mode: 'multiRow' }}
  onDataChange={nextData => setData(nextData)}
/>
```

### EditGrid ref 方法（常用）

| 方法 | 说明 |
|------|------|
| `addRow(record?, options?)` | 末行新增，`options.edit:true` 立即进入编辑 |
| `addRowFirst(record?)` | 首行新增 |
| `addRowAfter(rowKey, record?)` | 在指定行后插入 |
| `deleteRows(rowKeys)` | 删除一行或多行 |
| `validate(rowKey?)` | 校验全部行或指定行，返回 `Promise<boolean>` |
| `getData()` | 获取全部数据（不含内部字段） |
| `getChangedRows()` | 获取变更行（新增+修改+删除） |
| `getAddedRows()` / `getUpdatedRows()` / `getDeletedRows()` | 分类获取变更 |
| `updateCellValue(rowKey, field, value)` | 更新单个单元格 |
| `clearEditRows()` | 清空所有编辑态和草稿 |
| `getSelectedRowKeys()` | 获取已选行 key |

### editable 条件编辑

```jsx
// 按行数据条件决定
{ editable: (record) => record.status !== 'locked' }

// 整列不可编辑
{ editable: false }
```

### 保存提交模式（提交时统一校验）

```jsx
const handleSave = async () => {
  const valid = await editRef.current.validate();
  if (!valid) return;
  const changed = editRef.current.getChangedRows();
  await api.batchSave(changed);
};
```

### 基本用法（顶层包裹）

```jsx
import { ProConfigProvider } from 'tne-tinpernextpro-fe';

function App() {
  return (
    <ProConfigProvider locale={currentLang}>
      <RouterApp />
    </ProConfigProvider>
  );
}
```

### 远程语言包加载（企业级）

```jsx
<ProConfigProvider
  pack={localLangPack}
  groupCode="YMS"
  getRemoteResources={async (locale) => {
    const url = `${langFolderSrc}/${locale.replace(/-/g, '_')}.json`;
    const { data } = await axios.get(url);
    return { [localeKey]: mergedLangObject };
  }}
>
  {children}
</ProConfigProvider>
```

**关键 props**:

| 属性 | 说明 |
|------|------|
| `locale` | 当前语言标识（如 `'zh-CN'`） |
| `pack` | 本地语言包对象 |
| `groupCode` | 租户/应用编码，用于远程语言包分组 |
| `getRemoteResources` | 异步函数，接收 locale 返回语言包对象 |
