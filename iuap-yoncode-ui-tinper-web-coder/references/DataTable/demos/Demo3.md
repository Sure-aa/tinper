---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## 操作行携带简单搜索
继承于TinperNext-Table组件。

```tsx
import React, { useState, useRef } from "react";
import { Button, Space, Input } from '@tinper/next-ui';
import { services } from './mockData';
import { DataTable } from 'tne-tinpernextpro-fe'

function Demo1 () {
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);
  const tableRef = useRef(null);

  // 输出模拟数据

  const data = services;
  const columns = [
    {
      dataIndex: "name",
      title: "微服务名称",
      cardTitle: "name",
      type: "link",
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
    console.log(selectedRowKeys, tableRef.current.getSelectedRowKeys(), tableRef.current.getSelectedRowData(), "batchDel");
  }

  // const DataTable = (props) => {
  //   return <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable" {...props}/>
  // }

  return <div style={{ height: '50vh' }}>
    <DataTable
      ref={tableRef}
      
      showModeSwitch={true}
      renderToolBar={() => {
        return <div style={{ width: "100%", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <Input type='search' style={{ width: 300 }} placeholder="请输入名称" allowClear/>
          <Space>
            <Button type="primary">新增</Button>
            <Button onClick={batchDel}>批量删除</Button>
          </Space>
        </div>
      }}
      data={data}
      rowKey="id"
      columns={columns}
      showRowNum
      borderd
      operationType="button"
      fillSpace={true}
      operationItems={[
        { key: "edit", text: "编辑", onClick: (record, index) => {
          console.log(record, index, "edit")
        } },
        { key: "del", text: "删除" },
        { key: "auth", text: "授权", onClick: (record, index) => {
          console.log(record, index, "auth")
        } }
      ]}
      operationClick={operationClick}
      pagination={true}
      itemType={"horizontal"}
      rowSelection={ {
        type: "checkbox",
        selectedRowKeys,
        onChange: onChangeSelected
      }
      }
      onRowClick={onRowClick}
    />

  </div>
}

export default Demo1;
```
