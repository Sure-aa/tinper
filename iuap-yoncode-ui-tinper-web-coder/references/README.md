---
tags:
  - TinperNextPro
---
# TinperNextPro - 企业级高级业务组件库

> 基于 **@tinper/next-ui** 的企业级高级业务组件库
>
> 提供表单、表格、参照等复杂业务场景的开箱即用解决方案

**官方包名称**: `tne-tinpernextpro-fe` 【V3R6 环境包名称为 `ynf-tinper-next-pro`】

---

## 组件库说明

### 关于 TinperNextPro

TinperNextPro 是基于 **@tinper/next-ui** 基础组件库封装的高级业务组件库，提供了大量企业应用开发中常用的复杂业务组件。

**与基础组件库的关系**:

| 组件库 | 定位 | 包含内容 |
|-------|------|---------|
| **@tinper/next-ui** | 基础 UI 组件库 | Button、Input、Table 等基础组件 |
| **tne-tinpernextpro-fe** | 高级业务组件库 | DataForm、EditTable、DataGrid、EditGrid、TinperGrid、RefTable 等业务组件 |

**依赖关系**: TinperNextPro 依赖 @tinper/next-ui，使用时需要同时安装基础组件库。

### 安装方式

> 📦 **双重支持**: 本组件库支持 **TNS 加载**（推荐）和 **ynpm 安装** 两种方式

**加载方式说明**:
- **TNS 方式**（推荐）: 通过 TNS（统一前端NGINX服务）进行资源托管与管理，无需本地安装
- **ynpm 方式**: 通过 ynpm 从用友内部私有 npm 仓库安装
- **内网专用**: 两种方式均需在用友内网环境使用

---

## 核心特性

- **🎯 业务场景覆盖** - 20+ 高级业务组件，覆盖表单、表格、参照等企业级场景
- **📦 按需加载** - 支持直接引入和模块联邦两种加载方式
- **🔧 TypeScript** - 完整的 TypeScript 类型定义
- **🎨 高度可定制** - 丰富的配置项和自定义能力
- **🌍 国际化** - 内置多语言支持
- **⚡ 高性能** - 支持大数据表格、虚拟滚动等性能优化

---

## 快速开始

### 安装 / 接入

本组件库支持两种使用方式，推荐使用 **TNS 方式**（无需本地安装）。

#### 方式一：TNS 加载（推荐）

> 🌟 **推荐方式**: `tne-tinpernextpro-fe` 作为二方包提供，通过 TNS（统一前端NGINX服务）进行资源托管与管理。

**前置条件**:
- 项目已接入 TNS
- 参考 [YNF二方包管理及接入指南](https://docs.yonyoucloud.com/l/77c3ca1ecb16)
- 参考 [TNS接入指南](https://docs.yonyoucloud.com/l/4cde7dc9E79f)

**TNS 方式优势**:
- ✅ 无需本地安装，减少项目依赖体积
- ✅ 组件库统一托管，版本更新无需重新安装
- ✅ 支持动态加载，按需引入组件
- ✅ 更好的版本管理和统一升级

---

#### 方式二：ynpm 本地安装

> 💡 **备选方式**: 通过 ynpm 安装到本地 node_modules，适用于无法接入 TNS 的项目

**安装步骤：**

```bash
# 1. 首先全局安装 ynpm 工具
npm install ynpm-tool -g

# 2. 使用 ynpm 安装组件库（官方包名称）
ynpm install tne-tinpernextpro-fe --save

# 3. 同时需要安装基础组件库（如果项目中未安装）
ynpm install @tinper/next-ui --save
```

**为什么不能使用 npm？**

- 本组件库发布在用友内部私有 npm 仓库
- npm 默认连接的是公共 npm 仓库，无法访问内部包
- ynpm 工具自动配置内部仓库地址，确保正确安装

**常见问题：**

```bash
# ❌ 错误方式（无法安装）
npm install tne-tinpernextpro-fe --save

# ✅ 正确方式
ynpm install tne-tinpernextpro-fe --save
```

---

### 使用示例

TNS 加载和本地安装使用方式一样，直接通过tne-tinpernextpro-fe 引入即可：


```javascript
import { DataForm, DataTable, EditTable, SearchForm } from "tne-tinpernextpro-fe";

function MyComponent() {
  return (
    <DataForm formLayout="auto">
      <DataForm.Item label="用户名" name="username" inputType="input" />
      <DataForm.Item label="邮箱" name="email" inputType="input" />
    </DataForm>
  );
}
```


---

## 组件分类

### 1. 表单组件 (Form Controls)

#### DataForm - 数据表单

**功能说明**: 快速构建企业级表单，支持自适应布局、多种表单控件类型、字段校验、编辑/浏览态切换等功能。

**核心特性**:
- ✅ 自适应布局：根据容器宽度自动调整列数（1920px: 5列、1360px: 4列、1080px: 3列）
- ✅ 20+ 种内置表单项：input、number、date、select、cascader、treeselect、upload 等
- ✅ 字段动态控制：支持 hiddenKeys、invisibleKeys、disabledKeys、requiredKeys
- ✅ 编辑/浏览态切换：formMode 支持 edit 和 browse 两种模式
- ✅ 完整的表单实例方法：getFieldsValue、setFieldsValue、validate 等
- ✅ Hook 支持：useFormInstance 获取表单实例，无需透传

**类型定义**:
```typescript
interface DataFormProps extends FormProps {
  readOnly?: boolean;
  disabled?: boolean;
  formLayout?: 'auto' | number;
  hiddenKeys?: string[];
  invisibleKeys?: string[];
  requiredKeys?: string[];
  disabledKeys?: string[];
  values?: Record<string, any>;
  formMode?: 'edit' | 'browse';
  labelWidth?: number;
}
```

**关键属性**:
- `formLayout`: 表单列布局，'auto' 自适应 或 固定列数（如 3）
- `formMode`: 表单模式，'edit' 编辑态 或 'browse' 浏览态
- `hiddenKeys`: 隐藏的字段，依然会收集和校验
- `requiredKeys`: 必填字段数组
- `labelWidth`: 统一设置 label 宽度

**适用场景**: 详情页、编辑页、新增页等需要表单数据录入的场景

**使用示例**:
```javascript
function UserForm() {
  const formRef = useRef();

  return (
    <DataForm
      ref={formRef}
      formLayout="auto"
      labelWidth={100}
      initialValues={{ username: '张三' }}
    >
      <DataForm.Item
        label="用户名"
        name="username"
        inputType="input"
        required
      />
      <DataForm.Item
        label="年龄"
        name="age"
        inputType="number"
        editOptions={{ min: 1, max: 150 }}
      />
      <DataForm.Item
        label="生日"
        name="birthday"
        inputType="date"
      />
      <DataForm.Item
        label="部门"
        name="dept"
        inputType="select"
        editOptions={{
          options: [
            { label: '技术部', value: '1' },
            { label: '产品部', value: '2' }
          ]
        }}
      />
    </DataForm>
  );
}
```

---

#### SearchForm - 查询表单

**功能说明**: 专为查询场景设计的表单组件，继承 DataForm 的所有能力，额外提供查询特定功能。

**核心特性**:
- ✅ 展开/折叠功能：优化空间利用，支持配置默认展示行数
- ✅ 实时搜索模式：instant 属性开启实时搜索
- ✅ 已选条件展示：自动展示已选条件，可快速清除
- ✅ 逻辑运算符：支持 compareLogic 配置（等于、大于、小于、between 等）
- ✅ 内置操作按钮：查询、重置按钮及相关逻辑
- ✅ 高级设置（TODO）：可配置显示/隐藏字段

**类型定义**:
```typescript
interface SearchFormProps extends DataFormProps {
  collapsedNumber?: number;
  defaultCollapsed?: boolean;
  onCollapse?: (collapsed: boolean) => void;
  configurable?: boolean;
  searchType?: 'simple' | 'normal';
  submitter?: boolean | SubmitterProps;
  onSearch?: (values: any, errors: any, info: any) => void;
  onReset?: (values: any, formIns: any) => void;
  showSelected?: boolean;
  instant?: boolean;
}

interface SubmitterProps {
  searchConfig?: { submitText?: string; resetText?: string };
  render?: (props: any, doms: JSX.Element[]) => React.ReactNode[];
}
```

**关键属性**:
- `collapsedNumber`: 折叠时显示的行数（默认 1）
- `defaultCollapsed`: 默认是否折叠（默认 true）
- `searchType`: 查询表单类型，'normal' 或 'simple'
- `onSearch` / `onReset`: SearchForm 根属性中的查询与重置回调
- `submitter`: 提交按钮区配置，仅用于按钮文本、渲染定制或隐藏按钮区
- `showSelected`: 是否显示已选条件（默认 true）
- `instant`: 是否开启实时搜索（默认 false）

**适用场景**: 列表页的查询区域、数据筛选场景

**使用示例**:
```javascript
function SearchArea() {
  const searchRef = useRef();

  const handleSearch = (values, errors, { isReset }) => {
    console.log('查询条件:', values);
    console.log('是否重置:', isReset);
    // 执行查询逻辑
  };

  return (
    <SearchForm
      ref={searchRef}
      formLayout={4}
      defaultCollapsed={true}
      collapsedNumber={1}
      onSearch={handleSearch}
      onReset={(values, formIns) => handleSearch(values, undefined, { isReset: true, formIns })}
      submitter={{
        searchConfig: {
          submitText: '查询',
          resetText: '重置'
        }
      }}
    >
      <SearchForm.Item
        label="产品名称"
        name="productName"
        inputType="input"
      />
      <SearchForm.Item
        label="价格区间"
        name="priceRange"
        inputType="inputNumberGroup"
        compareLogic="between"
        placeholder={["最小值", "最大值"]}
      />
      <SearchForm.Item
        label="创建日期"
        name="createDate"
        inputType="rangepicker"
        compareLogic="between"
      />
      <SearchForm.Item
        label="状态"
        name="status"
        inputType="select"
        editOptions={{
          options: [
            { label: '全部', value: '' },
            { label: '启用', value: '1' },
            { label: '禁用', value: '0' }
          ]
        }}
      />
    </SearchForm>
  );
}
```

---

### 2. 表格组件 (Data Table)

#### DataTable - 数据表格

**功能说明**: 功能全面的数据展示与操作组件，支持分页、排序、筛选等企业级表格所需的所有功能。

**核心特性**:
- ✅ 大数据支持：虚拟滚动，流畅渲染万级数据
- ✅ 固定功能：固定列、固定表头
- ✅ 列操作：列拖拽、列锁定、列过滤
- ✅ 数据操作：单列查询、单列过滤、合计行
- ✅ 自动填充：fillSpace 自动填满父级剩余空间
- ✅ 完整的分页支持

**关键属性**:
- `columns`: 表格列配置
- `dataSource`: 表格数据
- `fillSpace`: 自动填满父级剩余空间
- `pagination`: 分页配置
- `rowSelection`: 行选择配置

**适用场景**: 数据列表展示、数据管理等场景

---

#### EditTable - 编辑表格

**功能说明**: 支持行内编辑和行内表单编辑的表格组件，提供丰富的编辑能力和数据操作方法。

**核心特性**:
- ✅ 两种编辑模式：
  - `inline`: 行内单元格编辑
  - `inlineForm`: 行内展开表单编辑
- ✅ 10+ 种单元格编辑类型：input、number、select、date、switch、treeselect 等
- ✅ 丰富的行操作方法：
  - 增：addRow、addRowLast、addRowBefore、addRowAfter、addRowChild
  - 删：deleteData、clearAllData
  - 改：editRow、saveRowData、saveMultiCellData
  - 查：getAllData、getAddRows、getEditRows、getDeleteRows
- ✅ 单元格级别校验：支持 validator、pattern、required 等
- ✅ 单元格错误管理：updateCellError、getCellError、clearCellError
- ✅ 操作列配置：operationItems 配置编辑、保存、取消等操作
- ✅ 大数据模式：isBigData 开启大数据表格优化

**类型定义**:
```typescript
interface EditTableProps extends TableProps {
  type?: 'inline' | 'inlineForm';
  formProps?: DataFormProps;
  autoEditedByClickRows?: false | 'click' | 'hover';
  isBigData?: boolean;
  fillSpace?: boolean;
  isSingleFind?: boolean;
  isSum?: boolean;
  isDragColumn?: boolean;
  isFilterColumn?: boolean;
  isSort?: boolean;
  isSingleFilter?: boolean;
  operationItems?: OperationItem[] | ((record, index, isEdit, innerOps) => OperationItem[]);
  operationClick?: (record, item, e) => void;
  operationType?: 'button' | 'link' | ((items, record) => ReactNode);
}

interface EditColumnType extends ColumnType {
  editType?: 'input' | 'textarea' | 'select' | 'date' | 'time' | 'switch' |
             'treeselect' | 'number' | 'inputNumberGroup' | 'rangepicker' |
             'cascader' | 'radiogroup' | 'checkboxgroup' | 'custom';
  editOptions?: object | ((record, index, info) => object);
  editAbled?: boolean | ((record, index, column) => boolean);
  onCellChange?: (record, column, value) => void;
  renderFormItem?: (form, record, index, column) => ReactNode;
  validator?: (value, record, data, callback) => void;
  patternMsg?: string;
}
```

**关键属性**:
- `type`: 编辑类型，'inline' 或 'inlineForm'
- `autoEditedByClickRows`: 点击行进入编辑，false / 'click' / 'hover'
- `isBigData`: 是否开启大数据模式
- `operationItems`: 操作列按钮配置
- `columns[].editType`: 列的编辑类型
- `columns[].editAbled`: 列是否可编辑
- `columns[].editOptions`: 编辑组件的属性配置

**适用场景**: 需要快速编辑表格数据的场景，如订单明细、产品列表、费用明细等

**使用示例**:
```javascript
function ProductList() {
  const tableRef = useRef();

  const columns = [
    {
      title: '产品名称',
      dataIndex: 'name',
      width: 200,
      editType: 'input',
      editAbled: true,
      required: true,
      validator: (value, record, data, callback) => {
        if (!value) {
          callback('产品名称不能为空');
        } else {
          callback();
        }
      }
    },
    {
      title: '数量',
      dataIndex: 'quantity',
      width: 120,
      editType: 'number',
      editAbled: true,
      editOptions: {
        min: 1,
        max: 9999,
        precision: 0
      }
    },
    {
      title: '单价',
      dataIndex: 'price',
      width: 120,
      editType: 'number',
      editAbled: true,
      editOptions: {
        min: 0,
        precision: 2
      }
    },
    {
      title: '状态',
      dataIndex: 'status',
      width: 120,
      editType: 'select',
      editAbled: true,
      editOptions: {
        options: [
          { label: '启用', value: '1' },
          { label: '禁用', value: '0' }
        ]
      },
      render: (text, record, index, { column }) => {
        const options = column.editOptions.options;
        const item = options.find(o => o.value === text);
        return item ? item.label : '-';
      }
    },
    {
      title: '备注',
      dataIndex: 'remark',
      width: 200,
      editType: 'textarea',
      editAbled: true,
      editOptions: {
        rows: 2,
        maxLength: 200
      }
    }
  ];

  const handleAdd = () => {
    tableRef.current.addRow({
      rowData: [{
        id: Date.now(),
        name: '',
        quantity: 1,
        price: 0,
        status: '1',
        remark: ''
      }],
      callback: () => {
        console.log('添加成功');
      }
    });
  };

  const handleSave = () => {
    // 先验证
    tableRef.current.validate({
      callback: (errors) => {
        if (errors && Object.keys(errors).length > 0) {
          console.error('验证失败:', errors);
          return;
        }
        // 验证通过，获取数据
        const allData = tableRef.current.getAllData();
        const editRows = tableRef.current.getEditRows();
        const addRows = tableRef.current.getAddRows();
        const deleteRows = tableRef.current.getDeleteRows();

        console.log('所有数据:', allData);
        console.log('编辑的数据:', editRows);
        console.log('新增的数据:', addRows);
        console.log('删除的数据:', deleteRows);
      }
    });
  };

  return (
    <div>
      <div style={{ marginBottom: 16 }}>
        <Button onClick={handleAdd}>新增</Button>
        <Button onClick={handleSave} type="primary">保存</Button>
      </div>
      <EditTable
        ref={tableRef}
        rowKey="id"
        columns={columns}
        dataSource={[]}
        type="inline"
        operationItems={(record, index, isEdit, innerOperations) => {
          if (isEdit) {
            return innerOperations; // 编辑态显示内置的保存、取消按钮
          }
          return [
            { key: 'edit', text: '编辑' },
            { key: 'delete', text: '删除' }
          ];
        }}
        operationClick={(record, item, e) => {
          if (item.key === 'delete') {
            tableRef.current.deleteData({
              rowKey: record.id,
              callback: () => {
                console.log('删除成功');
              }
            });
          }
        }}
      />
    </div>
  );
}
```

---

#### TinperGrid - 原始 Grid 组件

**功能说明**: 直接暴露 `@tinper/grid` 原始 API 的 Grid 组件，无业务封装，适合需要完全控制 Grid 行为的场景。DataGrid 和 EditGrid 均基于 `@tinper/grid` 独立封装，TinperGrid 与它们是并列关系。

**核心特性**:
- ✅ 完整 Grid API：通过 `onReady(api)` 或 `ref.current.api` 直接访问所有 GridApi 方法
- ✅ 模块化能力：`PaginationModule`、`RowSelectionModule`、`ColumnSortModule`、`FilterModule`、`EditModule`、`TreeModule` 等按需注册
- ✅ 完整列定义：`columnDefs` 使用 `@tinper/grid` 原生 `ColumnDef`
- ✅ 自定义组件：`customComponents` 覆盖内置渲染器
- ✅ 行/列操作：行选择、行拖拽、行固定、列排序、列筛选、列设置、列查找等全部能力透出

**关键属性**: 见 `../TinperGrid/readme.md`

**导入方式**:
```javascript
import { Grid } from 'tne-tinpernextpro-fe/TinperGrid';
```

**适用场景**: 需要完全控制 Grid、自行管理请求/工具栏/操作列、或使用 DataGrid/EditGrid 未封装的原生 Grid 能力时

---

#### DataGrid - 新数据表格

**功能说明**: 直接基于 `@tinper/grid` 的数据表格组件，不经过 GridCompat，原生 Grid API 透传 + 业务能力语义化补齐。

**核心特性**:
- ✅ 基于 @tinper/grid：直接透传排序、过滤、列设置、行选择、行号、合计等原生能力
- ✅ data 驱动：数据通过 `data` 传入，服务端分页由调用方在 `pagination.onChange` 自取后回填
- ✅ 操作列：operations 配置，每项独立 onClick
- ✅ 视图模式：displayMode（表格/卡片/看板）+ cardConfig/kanbanConfig
- ✅ 搜索区：searchPanel（表格上方）
- ✅ 行激活/高亮：activeRowKeys + activeRowMode
- ✅ 查看已选：showSelectedFilter + showSelectedOnly
- ✅ 业务能力：表头/明细切换(sumSwitch)、二维表(table2D)、行号列(lineNo)、空状态(emptyConfig)、链接穿透(jointQuery)

**关键属性**:
- `columnDefs`: 列配置，使用 @tinper/grid 原生 ColumnDef
- `data`: 数据源（唯一数据入口，组件不内置异步请求）
- `pagination`: 分页配置
- `rowSelection`: 行选择配置
- `operations`: 操作列按钮配置

**适用场景**: 数据列表展示、数据管理等场景

---

#### EditGrid - 新编辑表格

**功能说明**: 直接基于 `@tinper/grid` 的编辑表格组件，不经过 GridCompat，原生 Grid API 透传 + 编辑能力语义化补齐。

**核心特性**:
- ✅ 三种编辑模式：
  - `inline`: 行内单元格编辑
  - `expandForm`: 展开表单编辑
  - `drawerForm`: 右侧抽屉编辑（未传 renderEditForm 时按可编辑列自动生成表单）
- ✅ 多种编辑触发方式：manual / click / hover
- ✅ 浏览态 `browseMode`、单行编辑 `singleEditRow`（默认开）、`fillSpace` 填满容器
- ✅ 内置编辑器 + 自定义注入：input/textarea/select/number/switch/date/rangePicker/cascader/treeselect 等；参照等任意组件通过 `editorComponents` 或列级 `editorProps.component`/`referComponent` 注入
- ✅ 丰富的行操作方法：
  - 增：addRow、addRowFirst、addRowLast、addRowBefore、addRowAfter、addRowChild
  - 删：deleteRows、clearData
  - 改：editRow、saveRow、cancelRow、updateRow、updateCellValue、updateColumn
  - 查：getData、getRowData、getCellValue、getChangedRows
- ✅ 单元格级别校验：rules 支持 required、pattern、validator
- ✅ 单元格错误管理：setCellError、getCellError、clearCellError
- ✅ 变更追踪：getAddedRows、getUpdatedRows、getDeletedRows、getChangedRows
- ✅ 操作列配置：operations + operationColumn + defaultOperationVisible

**关键属性**:
- `data`: 表格数据
- `columnDefs`: 列定义，扩展了 editable、editor、editorProps、rules
- `editMode`: 编辑模式，'inline' 或 'expandForm'
- `editTrigger`: 进入编辑态方式，'manual' / 'click' / 'hover'
- `operations`: 自定义操作项
- `onDataChange`: 数据变化回调

**适用场景**: 需要快速编辑表格数据的场景，如订单明细、产品列表、费用明细等

**使用示例**:
```javascript
function ProductList() {
  const tableRef = useRef();
  const [data, setData] = useState([]);

  const columnDefs = [
    {
      field: 'name',
      headerName: '产品名称',
      width: 200,
      editable: true,
      editor: 'input',
      rules: [{ required: true, message: '产品名称不能为空' }],
    },
    {
      field: 'quantity',
      headerName: '数量',
      width: 120,
      editable: true,
      editor: 'number',
      editorProps: { min: 1, max: 9999, precision: 0 },
    },
    {
      field: 'price',
      headerName: '单价',
      width: 120,
      editable: true,
      editor: 'number',
      editorProps: { min: 0, precision: 2 },
    },
    {
      field: 'status',
      headerName: '状态',
      width: 120,
      editable: true,
      editor: 'select',
      editorProps: {
        options: [
          { label: '启用', value: '1' },
          { label: '禁用', value: '0' },
        ],
      },
      render: text => {
        const map = { '1': '启用', '0': '禁用' };
        return map[text] || '-';
      },
    },
    {
      field: 'remark',
      headerName: '备注',
      width: 200,
      editable: true,
      editor: 'textarea',
      editorProps: { maxLength: 200 },
    },
  ];

  const handleAdd = () => {
    tableRef.current.addRow({
      id: Date.now().toString(),
      name: '',
      quantity: 1,
      price: 0,
      status: '1',
      remark: '',
    });
  };

  const handleSave = async () => {
    const valid = await tableRef.current.validate();
    if (!valid) return;

    const changedRows = tableRef.current.getChangedRows();
    console.log('变更数据:', changedRows);
  };

  return (
    <div>
      <Space style={{ marginBottom: 16 }}>
        <Button onClick={handleAdd}>新增</Button>
        <Button onClick={handleSave} type="primary">保存</Button>
      </Space>
      <EditGrid
        ref={tableRef}
        rowKey="id"
        data={data}
        columnDefs={columnDefs}
        editTrigger="click"
        operations={[
          { key: 'delete', text: '删除', onClick: (record) => tableRef.current.deleteRows([record.id]) },
        ]}
        operationColumn={{ width: 180, pinned: 'right' }}
        onDataChange={nextData => setData(nextData)}
      />
    </div>
  );
}
```

---

#### GridCompat - 兼容表格（导出名 Table）

**功能说明**: 内部直接渲染 `@tinper/grid` 高性能 Grid，外层加适配器把 `@tinper/next-ui` Table（wui-table，含 `multiSelect`/`sort`/`filterColumn`/`dragColumn`/`sum`/`bigData` 等 HOC 体系）的 API 翻译成 Grid API，供存量项目低成本迁移到虚拟滚动。

**核心特性**:
- ✅ Grid 内核：Canvas 虚拟滚动，流畅渲染万级数据
- ✅ wui-table API 兼容：`columns`/`dataIndex`/HOC 体系可直接复用
- ✅ 两种声明方式：语义化 prop（`rowSelection`/`enableSorting` 等）或 `compatConfig` 声明原 HOC
- ✅ 排序、过滤、行选择、分页、列设置、列查找、树形、行拖拽、合计、多级表头等

**定位提醒**: ⚠️ 这是**存量迁移组件**，新项目请用 `DataGrid`/`EditGrid`，不要把 GridCompat 当主力表格。命名辨析：`tne-tinpernextpro-fe` 的 `Table`（GridCompat）与 `@tinper/next-ui` 的 `Table`（wui-table）同名不同物。

**关键属性**: 见 `../GridCompat/readme.md`

**适用场景**: 已有 `@tinper/next-ui Table` / wui-table 代码，想升级到 Grid 性能而不愿大规模重写

---

#### RefTable - 参照表格

**功能说明**: 列表穿梭参照组件，用于从大量数据中选择需要的数据项。

**核心特性**:
- ✅ 单选/多选模式：type 支持 'radio' 和 'checkbox'
- ✅ 搜索功能：待选区支持简单搜索和高级搜索
- ✅ 前端/后端过滤：filterOption 前端过滤，onSearch 后端搜索
- ✅ 分页支持：支持前端分页和后端分页
- ✅ 穿梭选择：待选区 ↔ 已选区数据穿梭
- ✅ 快捷操作：全选、清空、单选、多选
- ✅ 表单集成：支持作为表单项使用，受控 value

**类型定义**:
```typescript
interface RefTableProps {
  type?: 'radio' | 'checkbox';
  title?: string | ReactNode;
  columns: ColumnType[];
  rowKey?: string;
  data: any[];
  searchContent?: ReactNode | (() => ReactNode);
  showSearch?: boolean;
  onSearchChange?: (searchWord: string) => void;
  onSearch?: (searchWord: string) => void;
  filterOption?: (searchWord: string, item: any, direction: string) => boolean;
  targetKeys?: string[];
  targetData?: any[];
  value?: any[];
  onChange?: (value: any[]) => void;
  labelInValue?: boolean;
  fieldNames?: { label: string; value: string };
  pagination?: boolean | object;
  show?: boolean;
  onOk?: (keys: string[], data: any[]) => void;
  onCancel?: (keys: string[], data: any[]) => void;
}
```

**关键属性**:
- `type`: 参照类型，'radio' 单选 或 'checkbox' 多选
- `columns`: 表格列配置
- `data`: 待选区数据源
- `targetKeys`: 已选区数据的 keys
- `labelInValue`: value 是否为对象数组格式
- `fieldNames`: 字段映射，{ label: 'name', value: 'id' }
- `onSearch`: 搜索回调，支持后端搜索

**适用场景**: 人员选择、部门选择、物料选择、客户选择等参照场景

**使用示例**:
```javascript
function UserSelector() {
  const refRef = useRef();
  const [value, setValue] = useState([]);

  const columns = [
    { title: '姓名', dataIndex: 'name', width: 120 },
    { title: '部门', dataIndex: 'dept', width: 150 },
    { title: '邮箱', dataIndex: 'email', width: 200 }
  ];

  const data = [
    { id: '1', name: '张三', dept: '技术部', email: 'zhangsan@example.com' },
    { id: '2', name: '李四', dept: '产品部', email: 'lisi@example.com' },
    { id: '3', name: '王五', dept: '设计部', email: 'wangwu@example.com' }
  ];

  return (
    <RefTable
      ref={refRef}
      type="checkbox"
      title="选择人员"
      rowKey="id"
      columns={columns}
      data={data}
      value={value}
      onChange={setValue}
      labelInValue={true}
      fieldNames={{ label: 'name', value: 'id' }}
      showSearch={true}
      onSearch={(searchWord) => {
        console.log('搜索:', searchWord);
        // 调用后端搜索接口
      }}
      pagination={{
        pageSize: 10,
        total: 100
      }}
    />
  );
}
```

---

### 3. 选择器组件 (Selector)

#### GroupCascader - 级联分组选择器

**功能说明**: 支持分组展示的级联选择器，适用于多层级分类或地区选择场景。

**核心特性**:
- ✅ 分组展示：支持多级分组（类似通讯录字母分组）
- ✅ 懒加载模式：loadDataFlag 开启懒加载
- ✅ 搜索功能：showSearch 开启搜索，支持搜索回调
- ✅ 自定义分组规则：isGroupNum 控制分组阈值

**类型定义**:
```typescript
interface GroupCascaderProps {
  options: GroupCascaderOption[];
  loadDataFlag?: boolean;
  searchValue?: SearchValueItem[];
  placeholder?: string;
  allowClear?: boolean;
  bordered?: boolean | 'bottom';
  align?: 'left' | 'center' | 'right';
  defaultValue?: any[];
  value?: any[];
  onChange?: (value: any[], selectedOptions: any[]) => void;
  onSearch?: (value: string, selectedOptions: any[]) => void;
  showSearch?: boolean;
  separator?: string;
}

interface GroupCascaderOption {
  label: string;
  value: any;
  groupTopKey?: string;      // 所属大分组
  groupContentKey?: string;  // 所属小分组
  isGroupNum?: number;       // 分组阈值
  children?: GroupCascaderOption[];
}
```

**关键属性**:
- `options`: 级联选项数据，支持分组配置
- `loadDataFlag`: 是否使用懒加载
- `searchValue`: 懒加载搜索后的回填数据
- `showSearch`: 是否显示搜索框
- `separator`: 分隔符，默认 '/ '

**适用场景**: 地区选择、分类选择等多层级数据选择场景

---

#### InputSelect - 下拉搜索框

**功能说明**: 结合输入框与表格选择的组件，支持动态搜索过滤和单选/多选。

**核心特性**:
- ✅ 表格选择：下拉展示表格形式的选项
- ✅ 搜索过滤：输入框支持搜索过滤
- ✅ 单选/多选：multiple 控制选择模式
- ✅ 自定义列：columns 配置表格列

**类型定义**:
```typescript
interface InputSelectProps {
  placeholder?: string;
  value?: string | string[];
  rowKey: string;
  labelKey?: string;
  columns: ColumnType[];
  dataSource: any[];
  showHeader?: boolean;
  multiple?: boolean;
  onChange?: (value: string | string[]) => void;
  onSearch?: (value: string) => void;
  disabled?: boolean;
  allowClear?: boolean;
  maxTagCount?: number;
  maxTagTextLength?: number;
}
```

**关键属性**:
- `columns`: 表格列配置
- `dataSource`: 表格数据
- `multiple`: 是否多选
- `rowKey`: 数据的唯一标识字段
- `labelKey`: 显示的字段，优先级大于 rowKey
- `onSearch`: 搜索回调

**适用场景**: 需要从表格数据中选择的场景，如商品选择、客户选择等

---

### 4. 输入组件 (Input Controls)

#### Editor - 富文本编辑器

**功能说明**: 基于 TinyMCE 的富文本编辑器，支持丰富的文本编辑功能和插件扩展。

**核心特性**:
- ✅ 40+ 种插件：table、image、media、code、link、lists 等
- ✅ 自定义工具栏：toolbar 配置工具栏按钮
- ✅ 图片上传：onUpload 配置图片上传接口
- ✅ 全屏编辑：fullscreen 插件支持全屏
- ✅ 只读模式：readonly 属性控制只读状态
- ✅ 主题定制：支持多种主题配置

**关键属性**:
- `onUpload`: 图片上传函数，返回图片 URL
- `init.plugins`: 启用的插件列表
- `init.toolbar`: 工具栏配置
- `readonly`: 是否只读
- `init.height`: 编辑器高度

**适用场景**: 文章编辑、公告发布、邮件编写等富文本编辑场景

---

#### Email - 邮箱输入框

**功能说明**: 专为邮箱输入设计的组件，提供常用邮箱域名提示和完整的校验功能。

**核心特性**:
- ✅ 域名提示：自动提示常用邮箱域名（@163.com、@qq.com 等）
- ✅ 格式校验：内置邮箱格式校验
- ✅ 自定义校验：customCheck 支持自定义校验规则
- ✅ 浏览态：browser 属性支持浏览态显示
- ✅ 校验反馈：onError、onSuccess 回调

**类型定义**:
```typescript
interface EmailProps {
  placeholder?: string;
  value?: string;
  onChange?: (val: string, valid: boolean) => void;
  bordered?: boolean | 'bottom';
  disabled?: boolean;
  readOnly?: boolean;
  check?: boolean;
  pattern?: RegExp;
  required?: boolean;
  customCheck?: (val: string) => boolean;
  onError?: (val: string, pattern: RegExp) => void;
  onSuccess?: (val: string) => void;
  emailDomainList?: string[];
  browser?: boolean;
  maxLength?: number;
}
```

**关键属性**:
- `check`: 是否开启校验
- `pattern`: 自定义校验正则
- `customCheck`: 自定义校验函数
- `emailDomainList`: 可选邮箱域名列表
- `browser`: 是否开启浏览态

**适用场景**: 用户注册、联系方式填写等需要输入邮箱的场景

---

#### Phone - 电话输入框

**功能说明**: 支持国内区号选择、主机号和分机号输入的电话号码组件。

**核心特性**:
- ✅ 区号选择：支持国内城市区号选择
- ✅ 主机号/分机号：分别输入主机号和分机号
- ✅ 格式校验：支持主机号和分机号格式校验
- ✅ 自定义数据源：domesticSource 自定义区号列表
- ✅ 浏览态：browser 支持浏览态显示
- ✅ 顺序切换：swapOrder 切换主机号分机号位置

**类型定义**:
```typescript
interface PhoneProps {
  value?: { H: string; E: string };
  cityCode?: string;
  onChange?: (value: { H: string; E: string }, type: 'H' | 'E' | 'cityCode', cityCode: string) => void;
  onCityCodeSelect?: (cityCode: string) => void;
  placeholder?: { H: string; E: string };
  disabled?: boolean;
  readOnly?: boolean;
  bordered?: boolean | 'bottom';
  noExtension?: boolean;
  hideCityCode?: boolean;
  check?: boolean;
  required?: boolean;
  regH?: RegExp;
  regE?: RegExp;
  swapOrder?: boolean;
  browser?: boolean;
  domesticSource?: { cityName: string; code: string }[];
}
```

**关键属性**:
- `value`: 电话号码值，{ H: 主机号, E: 分机号 }
- `cityCode`: 区号
- `noExtension`: 不显示分机号（默认 true）
- `hideCityCode`: 隐藏区号选择
- `swapOrder`: 切换主机号分机号位置
- `domesticSource`: 自定义区号数据源

**适用场景**: 联系方式填写、企业信息登记等需要输入固定电话的场景

---

#### Mobile - 手机号输入框

**功能说明**: 支持国际区号选择的手机号码输入组件，内置号码格式校验。

**核心特性**:
- ✅ 国际区号：支持 200+ 个国家/地区区号
- ✅ 格式校验：内置手机号格式校验
- ✅ 自定义区号：countryList 自定义区号列表
- ✅ 格式化显示：displayFormat 配置显示格式
- ✅ 浏览态：browser 支持浏览态显示

**类型定义**:
```typescript
interface MobileProps {
  value?: string;
  countryCode?: number;
  onChange?: (value: string, country_code: number, country: any) => void;
  onCountryChange?: (locale: string, code: number, country: any, mobile: string) => void;
  placeholder?: string;
  disabled?: boolean;
  readOnly?: boolean;
  bordered?: boolean | 'bottom';
  hideCountryCode?: boolean;
  check?: boolean;
  required?: boolean;
  validate?: (value: string) => boolean;
  browser?: boolean;
  displayFormat?: string;
  countryList?: { country: string; country_code: number }[];
}
```

**关键属性**:
- `countryCode`: 国家区号
- `countryList`: 自定义国家区号列表
- `displayFormat`: 失焦后的格式化显示
- `hideCountryCode`: 是否隐藏区号选择
- `validate`: 自定义输入限制

**适用场景**: 用户注册、个人信息管理等需要输入手机号的场景

---

#### Identity - 证件号输入框

**功能说明**: 支持多种证件类型的输入和格式化显示。

**核心特性**:
- ✅ 多种证件类型：身份证、军官证、护照、银行卡
- ✅ 格式化显示：自动格式化显示（如：### ### #### #### ####）
- ✅ 格式校验：支持证件号格式校验
- ✅ 自定义类型：idTypes 自定义证件类型
- ✅ 浏览态：browser 支持浏览态显示

**类型定义**:
```typescript
interface IdentityProps {
  value?: { idType: string; identity: string };
  onChange?: (value: { idType: string; identity: string; isSelectChange: boolean }) => void;
  onIdentityChange?: (value: { idType: string; identity: string }) => void;
  placeholder?: string;
  disabled?: boolean;
  readOnly?: boolean;
  bordered?: boolean | 'bottom';
  showSelect?: boolean;
  check?: boolean;
  required?: boolean;
  pattern?: RegExp;
  customCheck?: (val: string) => boolean;
  browser?: boolean;
  idTypes?: Record<string, { name: string; formatter: string }>;
}
```

**关键属性**:
- `value`: 证件号值，{ idType: 类型, identity: 号码 }
- `idTypes`: 证件类型配置
- `showSelect`: 是否显示证件类型选择
- `formatter`: 格式化规则

**默认证件类型**:
```javascript
{
  '1': { name: '身份证', formatter: '### ### #### #### ####' },
  '2': { name: '军官证', formatter: '##################' },
  '3': { name: '护照', formatter: '#### ####' },
  '4': { name: '银行卡', formatter: '#### #### #### ####' }
}
```

**适用场景**: 实名认证、个人信息登记等需要输入证件号的场景

---

#### InputMultilang - 多语言输入框

**功能说明**: 支持多语言内容输入和切换的组件。

**核心特性**:
- ✅ 多语言录入：支持多种语言内容录入
- ✅ 语言切换：快速切换不同语言
- ✅ 自定义语言：支持自定义语言列表

**适用场景**: 国际化应用中的多语言内容编辑

---

#### Map - 地图选点

**功能说明**: 统一封装高德/百度/谷歌三种地图服务商的选点/地址录入组件，支持地址检索、选点、经纬度回写、浏览态展示及多边形/圆形/导航等区域绘制。

**核心特性**:
- ✅ 三服务商统一 API：`mapType` 切换高德 / 百度 / 谷歌
- ✅ 地址检索与选点：`searchAddress`、弹窗选点、经纬度回写
- ✅ 浏览态：`browser` + `browserValueRender`
- ✅ 区域绘制：多边形 / 圆形 / 线路 / 导航路径（`deliveryMethod`）
- ✅ key 灵活配置：prop 传入或 `window` 全局回退

**前置依赖**: ⚠️ 必须配置对应服务商 key（`amapKey`/`baiduMapKey`/`googleMapKey`），否则只显示未配置提示。

**关键属性**: 见 `../Map/readme.md`

**适用场景**: 地址录入、位置选择、配送区域绘制等需要地图的场景

---

### 5. 导航组件 (Navigation)

#### LeftMenu - 左侧菜单

**功能说明**: 适用于应用侧边导航的菜单组件。

**适用场景**: 应用导航、功能菜单等

---

#### Link - 链接

**功能说明**: 增强的链接组件。

**适用场景**: 页面跳转、外链访问等

---

### 6. 其他组件 (Others)

#### ProConfigProvider - 全局配置

**功能说明**: 为组件库提供全局配置的能力，可统一配置主题、语言等。

---

#### PageGuide - 页面引导

**功能说明**: 为用户提供页面功能引导，帮助用户快速了解页面功能。

**适用场景**: 新功能引导、操作说明等

---

#### StepGuide - 步骤引导

**功能说明**: 分步骤引导用户完成复杂操作。

**适用场景**: 新手引导、复杂流程操作指引等

---

#### TableTransfer - 表格穿梭框

**功能说明**: 支持表格形式的数据穿梭选择组件。

**适用场景**: 权限配置、数据迁移等需要批量选择和移动数据的场景

---

## 组件速查表

### 按使用场景分类

| 场景 | 推荐组件 | 说明 |
|-----|---------|------|
| 详情页 | DataForm | 支持编辑/浏览态切换 |
| 新增/编辑页 | DataForm | 20+ 种表单控件 |
| 列表查询 | SearchForm | 支持展开/折叠、已选条件 |
| 数据展示（新建，首选） | DataGrid | 基于 @tinper/grid，分页/排序/筛选；仅用户指定才用 DataTable |
| 数据编辑（新建，首选） | EditGrid | 基于 @tinper/grid，行内编辑/子表/增删行；仅用户指定才用 EditTable |
| 基础/普通表格（新建，首选） | TinperGrid | 原始 Grid API，无业务封装；仅用户指定才用 Table |
| 改动项目已有表格 | 保持原组件 | 不替换为 Grid 系列，直接在原表上改 |
| 数据展示（用户指定旧表格） | DataTable | 支持分页、排序、筛选 |
| 旧 wui-table 升级到高性能 Grid（存量迁移） | GridCompat（Table） | Grid 内核 + wui-table API，仅存量迁移用，新项目用 DataGrid |
| 数据编辑（用户指定旧表格） | EditTable | 支持行内编辑 |
| 人员选择 | RefTable | 穿梭框选择 |
| 地区选择 | GroupCascader | 支持分组 |
| 商品选择 | InputSelect | 表格形式选择 |
| 富文本编辑 | Editor | 基于 TinyMCE |
| 邮箱输入 | Email | 自动提示域名 |
| 电话输入 | Phone | 区号+主机号+分机号 |
| 手机号输入 | Mobile | 国际区号选择 |
| 证件号输入 | Identity | 多种证件类型 |
| 地图选点 / 地址录入 | Map | 高德/百度/谷歌，需配置 key |

### 所有组件列表

| 组件名称 | 说明 | 主要特性 |
|---------|------|---------|
| DataForm | 数据表单 | 自适应布局、20+ 控件、编辑/浏览态 |
| SearchForm | 查询表单 | 展开折叠、已选条件、逻辑运算符 |
| DataTable | 数据表格 | 大数据、固定列、分页排序 |
| EditTable | 编辑表格 | 行内编辑、单元格校验、操作列 |
| TinperGrid | 原始 Grid 组件 | 完整 Grid API、无业务封装、按需注册模块 |
| DataGrid | 数据表格 | 基于 @tinper/grid、请求分页、操作列、卡片视图 |
| EditGrid | 编辑表格 | 基于 @tinper/grid、行内编辑、单元格校验、变更追踪 |
| GridCompat | 兼容表格（Table） | Grid 内核 + wui-table API、存量迁移专用 |
| RefTable | 参照表格 | 穿梭选择、搜索、分页 |
| GroupCascader | 级联分组选择器 | 分组展示、懒加载、搜索 |
| InputSelect | 下拉搜索框 | 表格选择、搜索过滤 |
| Editor | 富文本编辑器 | 40+ 插件、图片上传、全屏 |
| Email | 邮箱输入框 | 域名提示、格式校验 |
| Phone | 电话输入框 | 区号选择、主机号分机号 |
| Mobile | 手机号输入框 | 国际区号、格式校验 |
| Identity | 证件号输入框 | 多种类型、格式化 |
| InputMultilang | 多语言输入框 | 多语言录入、切换 |
| Map | 地图选点 | 高德/百度/谷歌、地址检索、选点、区域绘制 |
| LeftMenu | 左侧菜单 | 侧边导航 |
| Link | 链接 | 页面跳转 |
| ProConfigProvider | 全局配置 | 主题、语言配置 |
| PageGuide | 页面引导 | 功能引导 |
| StepGuide | 步骤引导 | 流程引导 |
| TableTransfer | 表格穿梭框 | 批量选择、数据迁移 |

---

## 最佳实践

### 1. 表单布局建议

**DataForm 布局优化**:
```javascript
// ✅ 推荐：使用 auto 自适应布局
<DataForm formLayout="auto">
  {/* 自动根据容器宽度调整列数 */}
</DataForm>

// ✅ 固定列数场景
<DataForm formLayout={3}>
  {/* 始终显示 3 列 */}
</DataForm>

// ✅ 文本域占满一行
<DataForm.Item
  label="详细描述"
  name="description"
  inputType="textarea"
  colSpan={24}  // 占满整行
  editOptions={{ rows: 4 }}
/>
```

### 2. 编辑表格性能优化

**EditTable 性能最佳实践**:
```javascript
// ✅ 大数据量开启大数据模式
<EditTable
  isBigData={true}
  dataSource={largeData}  // 10000+ 条数据
/>

// ✅ 合理控制可编辑列
const columns = [
  { title: 'ID', dataIndex: 'id', editAbled: false },  // 不可编辑
  { title: '名称', dataIndex: 'name', editAbled: true },  // 可编辑
];

// ✅ 使用函数控制编辑状态
{
  title: '价格',
  dataIndex: 'price',
  editAbled: (record, index, column) => {
    return record.status === '1';  // 只有启用状态可编辑
  }
}

// ✅ 自定义编辑组件注意性能
{
  title: '复杂字段',
  dataIndex: 'complex',
  renderFormItem: React.memo((form, record, index, column) => {
    return <CustomComponent />;
  })
}
```

### 3. 查询表单优化

**SearchForm 使用技巧**:
```javascript
// ✅ 合理设置折叠行数
<SearchForm
  collapsedNumber={1}  // 默认显示 1 行
  defaultCollapsed={true}  // 默认折叠
/>

// ✅ 实时搜索需要防抖
<SearchForm
  instant={true}
  onSearch={debounce((values) => {
    // 查询逻辑
  }, 500)}
/>

// ✅ 使用逻辑运算符
<SearchForm.Item
  label="价格"
  name="price"
  inputType="inputNumberGroup"
  compareLogic="between"  // 区间查询
  placeholder={["最小值", "最大值"]}
/>

// ✅ 复杂查询条件自定义渲染
<SearchForm.Item
  label="状态"
  name="status"
  inputType="select"
  selectedRender={(val, info) => {
    return `状态: ${val === '1' ? '启用' : '禁用'}`;
  }}
/>
```

### 4. 参照组件最佳实践

**RefTable 使用建议**:
```javascript
// ✅ 大数据量使用后端分页
<RefTable
  type="checkbox"
  data={currentPageData}  // 当前页数据
  pagination={{
    current: pageNum,
    pageSize: 20,
    total: totalCount,
    onChange: handlePageChange  // 翻页时请求数据
  }}
  onSearch={(searchWord) => {
    // 后端搜索
    fetchData({ keyword: searchWord });
  }}
/>

// ✅ 小数据量使用前端过滤
<RefTable
  type="radio"
  data={allData}  // 全部数据
  filterOption={(searchWord, item, direction) => {
    return item.name.includes(searchWord);
  }}
/>

// ✅ 回显数据处理
<RefTable
  value={selectedValues}
  labelInValue={true}  // 返回 { label, value } 格式
  fieldNames={{
    label: 'userName',  // 映射到 userName 字段
    value: 'userId'     // 映射到 userId 字段
  }}
/>
```

### 5. 组件通用建议

**通用最佳实践**:

```javascript
// ✅ 使用 ref 获取组件实例
const formRef = useRef();
const tableRef = useRef();

// 表单操作
formRef.current.getFieldsValue();
formRef.current.setFieldsValue({ name: '张三' });
formRef.current.validate();

// 表格操作
tableRef.current.getAllData();
tableRef.current.addRow({ rowData: [...] });
tableRef.current.validate({ callback: (errors) => {...} });

// ✅ 使用 Hook 简化代码（无需透传 ref）
import { useFormInstance } from 'tne-tinpernextpro-fe';

function CustomFormItem() {
  const form = useFormInstance();  // 直接获取表单实例
  const values = form.getFieldsValue();
  return <div>{values.name}</div>;
}

// ✅ 使用 fieldid 便于测试定位
<DataForm fieldid="user-form">
  <DataForm.Item fieldid="username" name="username" />
</DataForm>

// 生成的 DOM 结构
<div id="user-form">
  <div id="user-form_username">...</div>
</div>

// ✅ 浏览态使用
<Email
  value="user@example.com"
  browser={true}  // 浏览态，只读显示
  browserStyle={{ color: '#1890ff' }}
/>

<Mobile
  value="13800138000"
  browser={true}
  customRender={(value, countryCode, country) => {
    return `${countryCode} ${value}`;
  }}
/>
```

---

## TypeScript 支持

完整的类型定义，支持智能提示和类型检查：

```typescript
import type {
  DataFormProps,
  DataFormInstance,
  SearchFormProps,
  EditTableProps,
  RefTableProps
} from 'tne-tinpernextpro-fe';

// 表单实例
const formRef = useRef<DataFormInstance>(null);

// 组件属性
const formProps: DataFormProps = {
  formLayout: 'auto',
  labelWidth: 100,
  initialValues: {}
};

// 表格列类型
import type { EditColumnType } from 'tne-tinpernextpro-fe';

const columns: EditColumnType[] = [
  {
    title: '名称',
    dataIndex: 'name',
    editType: 'input',
    editAbled: true
  }
];
```

---

## API 文档

每个组件都有详细的 API 文档，包含：
- **组件属性（Props）**: 完整的属性列表和类型定义
- **实例方法（Methods）**: 通过 ref 调用的方法
- **事件回调（Events）**: 各种事件的回调函数
- **类型定义（TypeScript）**: 完整的 TS 类型声明

请查看各组件目录下的 `readme.md` 文件获取详细文档。

**文档目录结构**:
```
tinper-next-pro/
├── DataForm/
│   ├── readme.md          # API 文档
│   └── demos/             # 示例代码
│       ├── Demo1.md       # 基础使用
│       ├── Demo2.md       # 高级用法
│       └── ...
├── EditTable/
│   ├── readme.md
│   └── demos/
├── SearchForm/
│   ├── readme.md
│   └── demos/
└── ...
```

---

## 相关链接

- **TinperNext UI 官网**: https://yondesign.yonyoucloud.com/website/
- **YNF二方包管理指南**: https://docs.yonyoucloud.com/l/77c3ca1ecb16
- **TNS接入指南**: https://docs.yonyoucloud.com/l/4cde7dc9E79f

---

## 常见问题 FAQ

### Q1: TNS 方式和 ynpm 安装方式有什么区别？

**A**: 两种方式各有特点，推荐使用 TNS 方式：

| 特性 | TNS 方式（推荐） | ynpm 安装方式 |
|-----|----------------|-------------|
| 本地安装 | ❌ 不需要 | ✅ 需要安装到 node_modules |
| 项目依赖体积 | 小（动态加载） | 大（打包到项目） |
| 版本更新 | 自动更新 | 需要手动更新 |
| 使用方式 | YNFLoader 加载 | 直接 import 引入 |
| 适用场景 | 已接入 TNS 的项目 | 无法接入 TNS 的项目 |

**使用建议**:
- 新项目优先使用 TNS 方式
- 已有项目可根据实际情况选择

### Q2: 如何选择使用哪种方式？

**A**: 根据项目情况选择：

```
是否已接入 TNS？
├─ 是 → 使用 TNS 方式（推荐）
│      优势：无需安装、自动更新、减少依赖体积
│
└─ 否 → 有两种选择：
       ├─ 接入 TNS → 使用 TNS 方式
       └─ 使用 ynpm 安装 → 传统方式
```

### Q3: 为什么不能使用 npm 安装？

**A**: 本组件库发布在用友内部私有 npm 仓库，npm 公共仓库无法访问。如果选择本地安装方式，必须使用 ynpm 工具:

```bash
# ❌ 无法安装
npm install tne-tinpernextpro-fe

# ✅ 正确方式
npm install ynpm-tool -g         # 先安装 ynpm
ynpm install tne-tinpernextpro-fe  # 使用 ynpm 安装
```

### Q4: 使用 ynpm 安装时提示 "404 Not Found" 怎么办？

**A**: 这说明你使用了 npm 而不是 ynpm。请确保：
1. 已安装 ynpm 工具: `npm install ynpm-tool -g`
2. 使用 ynpm 安装: `ynpm install tne-tinpernextpro-fe`
3. 如果还有问题，检查是否在用友内网环境

### Q5: 可以在外网环境使用吗？

**A**: 不可以。本组件库仅限用友内部使用，需要：
- 连接用友内网（TNS 和 ynpm 都需要）
- TNS 方式需要项目已接入 TNS
- ynpm 方式需要使用 ynpm 工具安装
- 外网环境无法访问内部资源

### Q6: TinperNextPro 和 @tinper/next-ui 是什么关系？

**A**: TinperNextPro 是基于 @tinper/next-ui 基础组件库封装的高级业务组件库：
- **@tinper/next-ui**: 基础 UI 组件（Button、Input、Table 等）
- **tne-tinpernextpro-fe**: 高级业务组件（DataForm、EditTable、RefTable 等）

**依赖关系**:
- TNS 方式：组件库自动处理依赖，无需关心
- ynpm 方式：需要同时安装基础组件库 `@tinper/next-ui`

### Q7: DataForm 和 SearchForm 有什么区别？

**A**: SearchForm 继承 DataForm 的所有能力，并额外提供查询特定功能：

| 特性 | DataForm | SearchForm |
|-----|---------|-----------|
| 基础表单能力 | ✅ | ✅ |
| 展开/折叠 | ❌ | ✅ |
| 已选条件展示 | ❌ | ✅ |
| 逻辑运算符 | ❌ | ✅ |
| 内置查询按钮 | ❌ | ✅ |

**使用建议**: 详情页用 DataForm，查询区域用 SearchForm。

### Q8: EditTable 如何实现复杂的编辑逻辑？

**A**: EditTable 提供多种方式实现复杂编辑：

```javascript
// 1. 使用 editAbled 函数控制可编辑状态
{
  title: '价格',
  dataIndex: 'price',
  editAbled: (record, index, column) => {
    return record.type === '1';  // 只有特定类型可编辑
  }
}

// 2. 使用 editOptions 函数实现联动
{
  title: '城市',
  dataIndex: 'city',
  editType: 'select',
  editOptions: (record, index, { isEdit }) => {
    // 根据省份动态加载城市
    const cities = getCitiesByProvince(record.province);
    return { options: cities };
  }
}

// 3. 使用 renderFormItem 自定义编辑组件
{
  title: '复杂字段',
  dataIndex: 'complex',
  renderFormItem: (form, record, index, column) => {
    return <CustomComplexInput />;
  }
}

// 4. 使用 onCellChange 监听单元格变化
{
  title: '数量',
  dataIndex: 'quantity',
  onCellChange: (record, column, value) => {
    // 数量变化时自动计算金额
    const price = record.price;
    const amount = value * price;
    tableRef.current.saveMultiCellData({
      rowData: { ...record, amount }
    });
  }
}
```

### Q9: 如何自定义表单控件类型？

**A**: DataForm 支持通过 `inputType="custom"` 自定义表单控件：

```javascript
<DataForm.Item
  label="自定义控件"
  name="custom"
  inputType="custom"
  render={(props) => {
    // props 包含 value、onChange 等
    return (
      <CustomInput
        value={props.value}
        onChange={props.onChange}
      />
    );
  }}
/>
```

**注意事项**:
- 自定义组件必须支持 `value` 和 `onChange` 属性
- 不能在组件内部使用 `defaultValue`，使用 Form 的 `initialValues`
- 需要调用 `onChange` 来同步表单值

### Q10: RefTable 如何处理大数据量？

**A**: RefTable 支持后端分页和搜索：

```javascript
<RefTable
  data={currentPageData}  // 只传当前页数据
  pagination={{
    current: pageNum,
    pageSize: 20,
    total: totalCount,
    onChange: (page, pageSize) => {
      // 请求对应页的数据
      fetchData({ page, pageSize });
    }
  }}
  onSearch={(searchWord) => {
    // 后端搜索
    fetchData({ keyword: searchWord });
  }}
  // 不要配置 filterOption，使用后端过滤
/>
```

### Q11: 如何统一配置组件的语言和主题？

**A**: 使用 ProConfigProvider 进行全局配置：

```javascript
import { ProConfigProvider } from 'tne-tinpernextpro-fe';

<ProConfigProvider
  locale="zh-cn"
  theme={{ primaryColor: '#1890ff' }}
>
  <App />
</ProConfigProvider>
```

---

## 问题反馈

遇到问题或有建议？欢迎通过以下方式反馈：

- **文档问题**: 查看各组件目录下的 readme.md 和 demos
- **使用问题**: 参考本文档的「最佳实践」和「常见问题」章节
- **Bug 反馈**: 联系组件库维护团队

---

## 更新日志

### v1.0.9
- 新增 Email、Phone、Mobile、Identity 输入组件
- 所有输入组件支持浏览态
- 优化组件 TypeScript 类型定义

### v1.0.6
- 新增 RefTable 参照表格组件
- DataForm 支持浏览态（formMode='browse'）
- SearchForm 支持实时搜索（instant）
- EditTable 优化大数据性能

### v1.0
- 发布初始版本
- 包含 DataForm、SearchForm、DataTable、EditTable 等核心组件

---

**提示**: 在使用组件之前，建议先浏览各组件目录下的 demos 示例，以便更好地了解组件的功能和使用方法。

遵循上述步骤，即可轻松集成并利用 TinperNextPro 高级组件，提升开发效率与页面质量。

---

**License**: MIT | **最后更新**: 2025-12-18

**重要提醒**：
- 📦 官方包名: `tne-tinpernextpro-fe`
- 🌟 推荐方式: TNS 加载
- 💡 备选方式: ynpm 本地安装 `ynpm install tne-tinpernextpro-fe`
- 🚫 不支持: npm 公共仓库无法访问
- 🔗 依赖组件: ynpm 方式需同时安装 `@tinper/next-ui`
- 🏢 使用限制: 仅限用友内网环境
