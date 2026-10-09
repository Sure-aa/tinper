---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## 表格完全受控（自定义控制数据以及分页信息）
继承于TinperNext-Table组件。

```tsx
import { SearchForm, DataTable } from 'tne-tinpernextpro-fe';
import React, { useState, useEffect, useCallback, useMemo } from "react";
import { Button, Space } from '@tinper/next-ui';
import { services } from './mockData';
const {ComponentLoader} = window.tnsSdk;

function Demo1 () {
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);

  const [page, setPage] = useState({ current: 1, pageSize: 20, total: 0 });
  const [data, setData] = useState([]);

  const mockedData = services;

  useEffect(() => {
    setData(mockedData.slice((page.current - 1) * page.pageSize, page.current * page.pageSize))
    setPage({
      ...page,
      total: mockedData.length
    })
  }, [mockedData])
  // 输出模拟数据

  // const data = mockedData;

  const searchContent = useMemo(() => (<SearchForm
    onValuesChange={onValuesChange}
    key="basic-search-form"
    formLayout={3}
    size="sm"
    onSearch={(values, errors, formIns) => { console.log('onSearch', values, errors, formIns) }}
    onReset={(values, formIns) => { console.log('onReset', values, formIns) }}
  >
    <SearchForm.Item htmlFor={false} inputType={"input"} label={"输入框"} name={"input"} />
    <SearchForm.Item htmlFor={false} inputType="number" label="数字框" name="number" />
    <SearchForm.Item htmlFor={false}
      inputType="inputNumberGroup"
      label="数字框组"
      name="numbergroup"
      placeholder={["请输入最小值", "请输入最大值"]}

      rules={[
        {
          min: 100,
          max: 200,
          message: "请输入100-200之间的数字"
        }
      ]}
    />
    <SearchForm.Item htmlFor={false} inputType="search" label="搜索框" name="search" />
    <SearchForm.Item htmlFor={false} inputType="select" label="下拉框" name="select" />
    <SearchForm.Item htmlFor={false} inputType="password" label="密码框" name="password" />
  </SearchForm>), [])

  const columns = [
    {
      dataIndex: "name",
      title: "微服务名称",
      cardTitle: "name",
      cardIndex: 1,
      sorter: "string"

    },
    {
      dataIndex: "code",
      title: "微服务编码",
      cardTitle: "微服务编码",
      cardIndex: 3,
      sorter: "string"
      // sorterClick,
      // getMultiSorterValue

    },

    {
      dataIndex: "pipelineName",
      title: "流水线名称",
      cardTitle: "流水线名称",
      cardIndex: 4

    },
    {
      dataIndex: "pipelineCode",
      title: "流水线编码",
      cardTitle: "流水线编码",
      cardIndex: 5

    },
    {
      dataIndex: "description",
      title: "描述",
      cardTitle: "描述",
      cardIndex: 6

    },
    {
      dataIndex: "img",
      title: "Img",
      ifshow: false,
      cardTitle: "Img",
      cardIndex: 2

    }
  ]

  function onChangeSelected (selectedRowKeys, selectedRows) {
    setSelectedRowKeys(selectedRowKeys)
  }

  function onRowClick (data, index, e) {
    console.log(data, index, e, "onRowClick")
  }

  function operationClick (record, eventInfo, e, index) {
    console.log(record, eventInfo, e, index, "operationClick");
  }

  function batchDel () {
    console.log(selectedRowKeys, "batchDel");
  }
  function onValuesChange (values) {
    console.log(values, "searchContent")
  }
  function onChange (params) {
    setData(mockedData.slice((params.current - 1) * params.pageSize, params.current * params.pageSize));
    setPage(params);
  }
  //  const DataTable = (props) => {
  //   return <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable" {...props}/>
  // }

  const renderToolBar = useCallback(() => {
      return <div style={{ width: "100%", display: "flex", justifyContent: "flex-end", alignItems: "center" }}>
        <Space>
          <Button type="primary">新增</Button>
          <Button onClick={batchDel}>批量删除</Button>
        </Space>
      </div>
  })

  return <div style={{ height: '60vh' }}>
    <ComponentLoader
      providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable"

      showModeSwitch={true}
      searchContent={searchContent}
      renderToolBar={renderToolBar}

      data={data}
      pagination={{
        ...page
      }}
      onChange={onChange}
      rowKey="id"
      columns={columns}
      showRowNum
      borderd
      operationType="button"
      fillSpace={true}
      operationItems={[
        { key: "edit", text: "编辑" },
        { key: "del", text: "删除" },
        { key: "auth", text: "授权" }
      ]}
      operationClick={operationClick}
      // pagination={true}
      itemType={"horizontal"}

      rowSelection={ {
        type: "checkbox",
        selectedRowKeys,
        onChange: onChangeSelected
      }
      }
      operationTypeProps={{
        maxCount: 1
      }}
      onRowClick={onRowClick}
    />

  </div>
}

export default Demo1;
```
