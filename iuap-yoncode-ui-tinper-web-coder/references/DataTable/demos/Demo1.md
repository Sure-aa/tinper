---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## DataTable.Column使用方式
继承于TinperNext-Table组件。

```tsx
import React from "react";
import { Button, Space } from '@tinper/next-ui';
import { services } from './mockData';
// const {ComponentLoader} = window.tnsSdk;

import {DataTable} from 'tne-tinpernextpro-fe';

function Demo1 () {
  const data = services;

  function operationClick (record, event, e, index) {
    console.log(record, event, e, index, "operationClick")
  }

  function sortFunc (_sortCol, data, _oldData) {
    console.log(_sortCol, data, _oldData, 'sortFunc')
  }

  function onRowClick (data, index, e) {
    console.log(data, index, e, "onRowClick")
  }
  // const DataTable = (props) => {
  //   return <YNFLoader providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable" {...props}/>
  // }

  return <div style={{ height: '50vh' }}>

    <DataTable
     
      showModeSwitch={true}
      renderToolBar={() => {
        return <div style={{ width: "100%", textAlign: "right" }}>
          <Space>
            <Button type="primary">新增</Button>
          </Space>
        </div>
      }}
      data={data}
      rowKey="id"
      borderd
      sort={{ mode: "single", backSource: false, sortFun: sortFunc }}
      pagination={true}
      itemType={"horizontal"}
      // itemType={"vertical"}
      operationTypeProps={{
        maxCount: 1
      }}
      rowActiveKeys

      operationClick={operationClick}
      onRowClick={onRowClick}
    >
      <DataTable.Column
        dataIndex= "name"
        title= "微服务名称"
        cardTitle= "微服务名称"
        cardIndex= {1}
        sorter="string"/>
      <DataTable.Column
        dataIndex= "code"
        title= "微服务编码"
        cardTitle= "微服务编码"
        cardIndex= {3}
        sorter="string"/>
      <DataTable.Column
        dataIndex= "pipelineName"
        title= "流水线名称"
        cardTitle= "流水线名称"
        cardIndex= {4}/>
      <DataTable.Column
        dataIndex= "pipelineCode"
        title= "流水线编码"
        cardTitle= "流水线编码"
        cardIndex= {5}/>
      <DataTable.Column
        dataIndex= "description"
        title= "描述"
        cardTitle= "描述"
        cardIndex= {6}/>
      <DataTable.Column
        dataIndex= "img"
        title= "Img"
        ifshow={false}
        cardTitle= "Img"
        cardIndex= {2}/>
    </DataTable>

  </div>
}

export default Demo1;
```
