---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## 多选以及带操作。
继承于TinperNext-Table组件。

```tsx
import React, { useState } from "react";
import { Button, Space, Clipboard } from '@tinper/next-ui';
import { services } from './mockData';

import { DataTable } from 'tne-tinpernextpro-fe'

function Demo1 () {
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);
  const [mode, setMode] = useState("table");

  const data = services;
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

  function changeMod (mode) {
    setMode(mode)
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

  // const DataTable = (props) => {
  //   return <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable" {...props}/>
  // }

  function success () {
    console.log('success');
  }
  function error () {
    console.log('error');
  }

  return <div style={{ height: '50vh' }}>
    <DataTable
      // providerPackage="tne-tinpernextpro-fe" 
      // providerEntry="DataTable"
      showModeSwitch={true}
      renderToolBar={() => {
        return <div style={{ width: "100%", textAlign: "right" }}>
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
        { key: "edit", text: "编辑" },
        {
          key: "copy",
          text: "复制名称",
          render: (record, index, childDom) => {
            return <Clipboard action="copy" text={record.name} success={success} error={error}>{childDom}</Clipboard>
          },
          hidden: false,
          onClick: (record) => {
            console.log(record, "click edit")
          },
          otherProps: {
            // disabled: true
          } },
        { key: "del", text: "删除" },
        { key: "auth", text: "授权" }
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
      rowActiveKeysMode={"single"}
      operationTypeProps={{
        maxCount: 4
      }}
      onRowClick={onRowClick}
    />

  </div>
}

export default Demo1;
```
