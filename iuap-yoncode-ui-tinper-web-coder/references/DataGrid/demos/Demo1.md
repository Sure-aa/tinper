---
tags:
  - TinperNextPro
  - DataGrid组件
---
# DataGrid 数据表格

## 基本使用
继承于Tinper-Grid组件。

```tsx
import React, { useMemo, useRef, useState } from 'react';
import { Button, Input, Space, Tag } from '@tinper/next-ui';
import {DataGrid} from 'tne-tinpernextpro-fe';

const allData = Array.from({ length: 86 }).map((_, index) => {
  const id = `${index + 1}`;
  const customer = ['用友网络', '星河制造', '北辰科技', '云启贸易'][Math.floor(index / 8) % 4];
  return {
    id,
    code: `SO-${String(index + 1).padStart(4, '0')}`,
    customer,
    amount: Math.round((index + 1) * 328.45),
    profit: Math.round((index + 1) * 87.35),
    status: ['待确认', '已确认', '已关闭'][index % 3],
    owner: ['张三', '李四', '王五'][index % 3],
    orderDate: `2026-05-${String((index % 28) + 1).padStart(2, '0')}`,
    description: `第 ${index + 1} 条销售订单，包含多列滚动、筛选、排序和卡片展示能力。`,
  };
});

const statusColorMap = {
  待确认: 'warning',
  已确认: 'success',
  已关闭: 'default',
};

const DataGridDemo = () => {
  const tableRef = useRef<any>(null);
  const [keyword, setKeyword] = useState('');
  const [selectedRowKeys, setSelectedRowKeys] = useState<string[]>([]);
  const [showSelectedOnly, setShowSelectedOnly] = useState(false);
  const [activeRowKeys, setActiveRowKeys] = useState<string[]>(['1']);
  const defaultSelectedData = useMemo(() => [allData[1]], []);

  const columnDefs = useMemo(() => [
    {
      field: 'code',
      headerName: '单据编号',
      width: 150,
      pinned: 'left',
      sortable: true,
      fieldType: 'link',
      filter: 'textFilter',
      filterParams: {
        showCaseSensitive: true,
      },
      render: (text: string) => <a>{text}</a>,
    },
    {
      field: 'customer',
      headerName: '客户',
      width: 180,
      filter: 'setFilter',
      filters: [
        { text: '用友网络', value: '用友网络' },
        { text: '星河制造', value: '星河制造' },
        { text: '北辰科技', value: '北辰科技' },
        { text: '云启贸易', value: '云启贸易' },
      ],
    },
    {
      field: 'amount',
      headerName: '金额',
      width: 120,
      align: 'right',
      sortable: true,
      fieldType: 'number',
      filter: 'numberFilter',
      sumPrecision: 2,
      sumThousandth: true,
      render: (text: number) => Number(text || 0).toLocaleString(),
    },
    {
      field: 'profit',
      headerName: '毛利',
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
      render: (text: number) => Number(text || 0).toLocaleString(),
    },
    {
      field: 'status',
      headerName: '状态',
      width: 120,
      filter: 'multiFilter',
      filters: [
        { text: '待确认', value: '待确认' },
        { text: '已确认', value: '已确认' },
        { text: '已关闭', value: '已关闭' },
      ],
      render: (text: keyof typeof statusColorMap) => (
        <Tag color={statusColorMap[text]}>{text}</Tag>
      ),
    },
    {
      field: 'owner',
      headerName: '负责人',
      width: 120,
      filter: 'textFilter',
      filterParams: {
        showCaseSensitive: true,
      },
    },
    {
      field: 'orderDate',
      headerName: '单据日期',
      width: 130,
      fieldType: 'date',
      filter: 'dateFilter',
    },
    {
      field: 'description',
      headerName: '说明',
      width: 320,
      filter: 'textFilter',
      filterParams: {
        showCaseSensitive: true,
      },
    },
  ], []);

  return (
    <>
      {/* DataGrid 不再内置 toolbar，表格级按钮放在组件外部，通过 ref 操作 */}
      <Space style={{ marginBottom: 12 }}>
        <Button colors="primary">新增</Button>
        <Button onClick={() => tableRef.current?.reload()}>刷新</Button>
        <Button onClick={() => console.log(tableRef.current?.getSelectedRows())}>获取已选数据</Button>
        <Button onClick={() => tableRef.current?.clearSelection()}>清空选择</Button>
        <Button onClick={() => tableRef.current?.setActiveRowKeys(['3'])}>激活第三行</Button>
      </Space>
      <DataGrid
        ref={tableRef}
        fieldid="datatable_grid_demo"
        rowKey="id"
        data={allData}
        columnDefs={columnDefs}
        selectedData={defaultSelectedData}
        activeRowKeys={activeRowKeys}
        onActiveRowKeysChange={keys => setActiveRowKeys(keys as string[])}
        pagination={{
          current: 1,
          pageSize: 10,
          showTotal: total => `共 ${total} 条`,
        }}
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
        enableFillRemainingWidth
        showRowNum={{ width: 58, pinned: 'left' }}
        rowHover={{
          enabled: true,
        }}
        rowSelection={{
          mode: 'multiRow',
          selectedRowKeys,
          onChange: event => setSelectedRowKeys(event.selectedKeys),
        }}
        showSelectedFilter
        showSelectedOnly={showSelectedOnly}
        onShowSelectedOnlyChange={setShowSelectedOnly}
        summary={{
          showSubtotal: true,
          subtotalLabelColumn: 'code',
          subtotalLabelText: '小计',
          subtotalColumns: ['amount', 'profit'],
          getSubtotalPosition: (rows: any[], index: number) => {
            return index === rows.length - 1 || rows[index].customer !== rows[index + 1]?.customer;
          },
          subtotalPinned: false,
          showTotal: true,
          totalLabelColumn: 'code',
          totalLabelText: '合计',
          totalColumns: ['amount', 'profit'],
          totalPinned: 'bottom',
          thousandth: true,
        }}
        searchPanel={(
          <Space>
            <Input
              value={keyword}
              style={{ width: 240 }}
              placeholder="搜索编号、客户、负责人"
              onChange={setKeyword}
            />
            <Button colors="primary" onClick={() => {
              tableRef.current?.api?.setTextFilter?.('code', 'contains', keyword);
              tableRef.current?.api?.applyFilters?.('code', 'text');
            }}
            >
              查询
            </Button>
            <Button onClick={() => {
              setKeyword('');
              tableRef.current?.api?.clearFilter?.();
            }}
            >
              重置
            </Button>
          </Space>
        )}
        displayModeSwitchVisible
        cardConfig={{
          titleField: 'code',
          statusField: 'status',
          showSelectAll: true,
          pageSize: 12,
        }}
        operations={[
          { key: 'view', text: '查看', onClick: record => console.log('view', record) },
          { key: 'edit', text: '编辑', onClick: record => console.log('edit', record) },
          {
            key: 'close',
            text: '关闭',
            hidden: record => record.status === '已关闭',
            onClick: record => console.log('close', record),
          },
        ]}
        operationColumn={{ width: 180, pinned: 'right' }}
        height={420}
        width={980}
      />
    </>
  );
};

export default DataGridDemo;
```
