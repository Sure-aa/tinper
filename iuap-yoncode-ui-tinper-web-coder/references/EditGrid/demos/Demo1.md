---
tags:
  - TinperNextPro
  - EditGrid组件
---
# EditGrid 编辑表格

## 基本使用
继承于Tinper-Grid组件。

```tsx
import React, { useMemo, useRef, useState } from 'react';
import { Button, Input, Space, Tag } from '@tinper/next-ui';
import EditGrid from 'tne-tinpernextpro-fe';

const initialData = [
  {
    id: '1',
    material: '机械键盘',
    category: 'office',
    qty: 5,
    price: 399,
    taxRate: 0.06,
    enabled: true,
    deliveryDate: '2026-05-10',
    remark: '青轴',
  },
  {
    id: '2',
    material: '会议白板',
    category: 'office',
    qty: 1,
    price: 899,
    taxRate: 0.13,
    enabled: false,
    deliveryDate: '2026-05-12',
    remark: '带支架',
  },
  {
    id: '3',
    material: '显示器',
    category: 'device',
    qty: 2,
    price: 1299,
    taxRate: 0.13,
    enabled: true,
    deliveryDate: '2026-05-16',
    remark: '24寸',
  },
  {
    id: '4',
    material: '云服务',
    category: 'service',
    qty: 12,
    price: 199,
    taxRate: 0.06,
    enabled: true,
    deliveryDate: '2026-05-20',
    remark: '包月',
  },
];

const categoryOptions = [
  { label: '办公用品', value: 'office' },
  { label: '电子设备', value: 'device' },
  { label: '服务采购', value: 'service' },
];

const getCategoryLabel = (value: string) => {
  return categoryOptions.find(item => item.value === value)?.label || '-';
};

const EditGridDemo = () => {
  const tableRef = useRef<any>(null);
  const [data, setData] = useState(initialData);
  const [selectedRowKeys, setSelectedRowKeys] = useState<string[]>([]);
  const [expandFormMode, setExpandFormMode] = useState(false);

  const columnDefs = useMemo(() => [
    {
      field: 'material',
      headerName: '物料名称',
      width: 180,
      pinned: 'left',
      sortable: true,
      filter: 'textFilter',
      filterParams: {
        showCaseSensitive: true,
      },
      editable: true,
      editor: 'input',
      editorProps: {
        placeholder: '请输入物料名称',
      },
      rules: [
        { required: true, message: '物料名称不能为空' },
      ],
    },
    {
      field: 'category',
      headerName: '分类',
      width: 150,
      filter: 'setFilter',
      filters: categoryOptions.map(item => ({
        text: item.label,
        value: item.value,
      })),
      editable: true,
      editor: 'select',
      editorProps: {
        options: categoryOptions,
      },
      render: (text: string) => getCategoryLabel(text),
    },
    {
      field: 'qty',
      headerName: '数量',
      width: 110,
      align: 'right',
      sortable: true,
      fieldType: 'number',
      filter: 'numberFilter',
      sumPrecision: 0,
      editable: true,
      editor: 'number',
      editorProps: {
        min: 1,
        precision: 0,
      },
      rules: [
        {
          validator: (value: number) => value > 0 ? undefined : '数量必须大于 0',
        },
      ],
    },
    {
      field: 'price',
      headerName: '单价',
      width: 120,
      align: 'right',
      sortable: true,
      fieldType: 'number',
      filter: 'multiFilter',
      filterParams: {
        multi: {
          primary: 'number',
        },
      },
      sumPrecision: 2,
      sumThousandth: true,
      editable: true,
      editor: 'number',
      editorProps: {
        min: 0,
        precision: 2,
      },
      render: (text: number) => `￥${Number(text || 0).toLocaleString()}`,
    },
    {
      field: 'taxRate',
      headerName: '税率',
      width: 100,
      align: 'right',
      fieldType: 'number',
      filter: 'numberFilter',
      editable: true,
      editor: 'number',
      editorProps: {
        min: 0,
        max: 1,
        precision: 2,
      },
      render: (text: number) => `${Math.round(Number(text || 0) * 100)}%`,
    },
    {
      field: 'enabled',
      headerName: '启用',
      width: 100,
      filter: 'setFilter',
      filters: [
        { text: '启用', value: true },
        { text: '停用', value: false },
      ],
      editable: true,
      editor: 'switch',
      render: (text: boolean) => (
        <Tag color={text ? 'success' : 'default'}>{text ? '启用' : '停用'}</Tag>
      ),
    },
    {
      field: 'deliveryDate',
      headerName: '交付日期',
      width: 130,
      fieldType: 'date',
      filter: 'dateFilter',
      editable: true,
      editor: 'date',
    },
    {
      field: 'remark',
      headerName: '备注',
      width: 220,
      filter: 'textFilter',
      filterParams: {
        showCaseSensitive: true,
      },
      editable: true,
      editor: 'custom',
      renderEditor: ({ value, setValue }) => (
        <Input
          type="textarea"
          rows={1}
          value={value}
          onChange={setValue}
        />
      ),
    },
  ], []);

  return (
    <div>
      <Space style={{ marginBottom: 12 }}>
        <Button
          colors="primary"
          onClick={() => tableRef.current?.addRow?.({
            material: '新增物料',
            category: 'office',
            qty: 1,
            price: 0,
            taxRate: 0.13,
            enabled: true,
            deliveryDate: '2026-05-25',
            remark: '',
          })}
        >
          新增行
        </Button>
        <Button onClick={() => tableRef.current?.validate?.()}>
          校验全部
        </Button>
        <Button onClick={() => tableRef.current?.addRowFirst?.({
          material: '首行物料',
          category: 'device',
          qty: 1,
          price: 100,
          taxRate: 0.13,
          enabled: true,
          deliveryDate: '2026-05-25',
          remark: '插入到首行',
        })}>
          首行新增
        </Button>
        <Button onClick={() => tableRef.current?.addRowAfter?.('2', {
          material: '插入物料',
          category: 'office',
          qty: 2,
          price: 50,
          taxRate: 0.06,
          enabled: true,
          deliveryDate: '2026-05-26',
          remark: '插入到第 2 行后',
        })}>
          行后新增
        </Button>
        <Button onClick={() => tableRef.current?.updateColumnDown?.('1', 'taxRate', 0.09, 2)}>
          向下填充税率
        </Button>
        <Button onClick={() => tableRef.current?.moveRows?.(['3'], '1', 'before')}>
          移动第 3 行到首行前
        </Button>
        <Button onClick={() => tableRef.current?.setCellError?.('1', 'material', '外部设置的单元格错误')}>
          设置错误
        </Button>
        <Button onClick={() => tableRef.current?.clearCellError?.()}>
          清空错误
        </Button>
        <Button onClick={() => setExpandFormMode(prev => !prev)}>
          {expandFormMode ? '切换行内编辑' : '切换展开表单'}
        </Button>
        <Button onClick={() => console.log(tableRef.current?.getChangedRows?.())}>
          获取变更行
        </Button>
        <Button onClick={() => console.log({
          added: tableRef.current?.getAddedRows?.(),
          updated: tableRef.current?.getUpdatedRows?.(),
          deleted: tableRef.current?.getDeletedRows?.(),
        })}
        >
          获取增改删
        </Button>
        <Button onClick={() => console.log(tableRef.current?.getData?.())}>
          获取全部数据
        </Button>
      </Space>
      <EditGrid
        ref={tableRef}
        fieldid="edittable_grid_demo"
        rowKey="id"
        data={data}
        columnDefs={columnDefs}
        editMode={expandFormMode ? 'expandForm' : 'inline'}
        editTrigger={expandFormMode ? 'manual' : 'click'}
        validateTrigger="onChange"
        renderEditForm={({ record, setRecord, save, cancel }) => (
          <Space style={{ padding: 12, width: '100%' }}>
            <Input
              value={record.material}
              style={{ width: 180 }}
              onChange={(value: string) => setRecord({ material: value })}
            />
            <Input
              value={record.remark}
              style={{ width: 260 }}
              onChange={(value: string) => setRecord({ remark: value })}
            />
            <Button colors="primary" onClick={save}>保存</Button>
            <Button onClick={cancel}>取消</Button>
          </Space>
        )}
        enableSorting
        enableFilter
        enableFind
        enableColumnSet
        enableHeaderColumnSizingMenu
        enablePinned
        columnSetOptions={{
          showFooter: true,
          showSelectAll: true,
          showSelected: true,
          showColumnAutoWidth: true,
          showColumnMover: true,
          showReset: true,
          showToTop: true,
          showLock: true,
        }}
        dragborder
        keepWidthBalance
        showRowNum={{ width: 58, pinned: 'left' }}
        summary={{
          showSubtotal: true,
          subtotalLabelColumn: 'material',
          subtotalLabelText: '小计',
          subtotalColumns: ['qty', 'price'],
          getSubtotalPosition: (rows: any[], index: number) => {
            return index === rows.length - 1 || rows[index].category !== rows[index + 1]?.category;
          },
          showTotal: true,
          totalLabelColumn: 'material',
          totalLabelText: '合计',
          totalColumns: ['qty', 'price'],
          totalPinned: 'bottom',
          thousandth: true,
        }}
        rowDrag={{
          enabled: true,
          onRowReorderEnd: event => console.log('onRowReorderEnd', event),
        }}
        rowSelection={{
          mode: 'multiRow',
          selectedRowKeys,
          onChange: event => setSelectedRowKeys(event.selectedKeys || []),
        }}
        operations={[
          {
            key: 'copy',
            text: '复制',
            hidden: (_record, _index, editing) => editing,
            onClick: record => tableRef.current?.addRow?.({
              ...record,
              id: `${Date.now()}`,
            }),
          },
        ]}
        operationColumn={{ width: 220, pinned: 'right' }}
        onDataChange={nextData => setData(nextData)}
        onRowSave={(record) => console.log('onRowSave', record)}
        onValidate={(valid, errors) => console.log('onValidate', valid, errors)}
        height={380}
        width={980}
      />
    </div>
  );
};

export default EditGridDemo;
```

---

## 注入业务编辑器（editorComponents）

`editorComponents` 按 `editor` 类型字符串**全局注册**自定义编辑组件，避免每列重复声明。参照、邮箱、手机、证件、链接等业务组件都可这样注入。优先级：**列级 `editorProps.component`/`referComponent` > 全局 `editorComponents[editor]` > 内置回退**。

```tsx
import {
  EditGrid,
  RefTable,
  Email,
  Mobile,
  Phone,
  Link,
  InputMultilang,
} from 'tne-tinpernextpro-fe';

// 全局注册：列的 editor 字符串命中这里的组件
const editorComponents = {
  reftable: RefTable,
  email: Email,
  mobile: Mobile,
  phone: Phone,
  link: Link,
};

const columnDefs = [
  {
    field: 'supplier', headerName: '供应商', editable: true,
    editor: 'reftable',                  // 命中 editorComponents.reftable → RefTable
    editorProps: {
      title: '选择供应商', rowKey: 'value', type: 'checkbox',
      columns: [{ dataIndex: 'label', title: '供应商', width: 160 }],
      data: [{ label: '华北智造', value: 'north' }, { label: '沪上电子', value: 'sh' }],
      fieldNames: { label: 'label', value: 'value' },
    },
    render: (value: any[]) => (value || []).map(i => i.label).join('、') || '-',
  },
  {
    field: 'contactEmail', headerName: '邮箱', editable: true,
    editor: 'email',                     // 命中 editorComponents.email → Email
    editorProps: { placeholder: '请输入邮箱', maxLength: 32 },
  },
  {
    field: 'mobilePhone', headerName: '手机号', editable: true,
    editor: 'mobile',
    editorProps: { countryCode: 86, displayFormat: '3 4 4' },
  },
  {
    field: 'i18nName', headerName: '多语名称', editable: true,
    editor: 'custom',
    editorProps: {
      component: InputMultilang,         // 列级直接注入，优先级最高
      valuePropName: 'localeList',
      changePropName: 'onChange',
      getValueFromChange: (_v, localeList) => localeList,
      locale: 'zh_CN',
    },
    render: (value: any) => value?.zh_CN || '-',
  },
];

<EditGrid
  rowKey="id"
  data={data}
  columnDefs={columnDefs}
  editorComponents={editorComponents}
  editTrigger="click"
/>
```

> `editor: 'reftable'` 等是任意字符串，由 `editorComponents[editor]` 解析为对应组件；`editorProps.valuePropName`/`changePropName`/`getValueFromChange` 适配非标准受控协议（如多语的 `localeList`）。需要完全自定义渲染时仍可用列级 `renderEditor`（优先级最高）。详见 `../readme.md` 的「自定义 / 参照编辑器」。
