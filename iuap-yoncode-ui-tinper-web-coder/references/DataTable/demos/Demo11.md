---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## 展开子表格
继承于TinperNext-Table组件。

```tsx
import React, { useState, useRef , useCallback} from "react";
import { Button, Space } from '@tinper/next-ui';
import { services } from './mockData';

import { DataTable, SearchForm } from 'tne-tinpernextpro-fe'
import { useMemo } from "react";

function Demo1 () {
  // 输出模拟数据
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);
  const [expandedRowKeys, setExpandedRowKeys] = useState([])
  const [childData, setChildData] = useState([])

  const [group, setGroup] = useState(1);

  const tableRef = useRef(null);

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
      sorter: "string",
      orderNum: 1,
      order: "descend"
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
      cardIndex: 5,
      sorter: (pre, after) => {
        return pre.a - after.a
      }

    },
    {
      dataIndex: "description",
      title: "描述",
      cardTitle: "描述",
      cardIndex: 6,
      sortEnable: true,
      sorterClick: (data, _type) => {
        // 排序后触发事件
        console.log("data", data);
      }

    },
    {
      dataIndex: "img",
      title: "Img",
      cardTitle: "Img",
      cardIndex: 2

    }
  ]
  function operationClick (record, event, e, index) {
    console.log(record, event, e, index, "operationClick")
  }

  function sortFunc (_sortCol, data, _oldData) {
    console.log(_sortCol, data, _oldData, 'sortFunc')
  }

  function onRowClick (data, index, e) {
    console.log(data, index, e, "onRowClick")
  }
  function onChangeSelected (selectedRowKeys, selectedRows) {
    setSelectedRowKeys(selectedRowKeys)
  }

  function request (params) {
    console.log(params, "allParams");
    return new Promise((res, rej) => {
      const { page } = params;
      const { current, pageSize } = page;
      res({
        success: true,
        data: data.slice((current - 1) * pageSize, (current) * pageSize),
        total: data.length
      })
    })
  }
  function requestNoPage (params) {
    console.log(params, "allParams");
    return new Promise((res, rej) => {
      res({
        success: true,
        data,
        total: data.length
      })
    })
  }
  function changeParams () {
    setGroup(Math.random().toString().slice(2, 4))
    console.log(tableRef.current.getQueryFilters())
  }
  function onValuesChange (values) {
    console.log(values, "searchContent")
  }
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
          max: 200
        }
      ]}
    />
    <SearchForm.Item htmlFor={false} inputType="search" label="搜索框" name="search" />
    <SearchForm.Item htmlFor={false} inputType="select" label="下拉框" name="select" />
    <SearchForm.Item htmlFor={false} inputType="password" label="密码框" name="password" />
  </SearchForm>), [])

  function onExpand (expanded, record) {
    if (expanded) {
      setChildData(services.slice(0, 10));
      setExpandedRowKeys([...expandedRowKeys, record.id])
    } else {
      setExpandedRowKeys(expandedRowKeys.filter(item => item !== record.id));
    }
  }

  function expandedRowRender (record) {
    return <DataTable fieldid={`ypr_baseline_installer_build_${record.id}_list`}
      data={services.slice(0, 4)}
      columns={columns}
      fillSpace={false}
      rowKey={rec => rec.id}
      handleScrollX={(a, b, e) => e && e.stopPropagation()}
    />
  }

  const renderToolBar = useCallback(() => {
     return <div style={{ width: "100%", textAlign: "right" }}>
          <Space>
            <Button type="primary">新增</Button>

          </Space>
        </div>
  })
  return <div style={{ height: '100vh' }}>

    <DataTable
      ref={tableRef}
      providerPackage="tne-tinpernextpro-fe" providerEntry="DataTable"
      showModeSwitch={true}
      searchContent={ searchContent}
      renderToolBar={renderToolBar}
      stripeLine
      // expandable
      // expandedRowKeys={expandedRowKeys}
      // onExpand={onExpand}
      expandedRowRender={expandedRowRender}
      // request={requestNoPage}
      request={request}

      rowKey="id"
      columns={columns}
      // bodyDisplayInRow={false}
      params={{ group }}
      showRowNum
      borderd
      fillSpace={true}
      isSingleFilter={true}

      sort={{ mode: "single", backSource: false, sortFun: sortFunc }}
      // pagination={true}
      itemType={"vertical"}
      rowSelection={ {
        type: "checkbox",
        selectedRowKeys,
        onChange: onChangeSelected
      }
      }
      filterMode="single"
      operationItems={[
        { key: "edit", text: "编辑" },
        { key: "del", text: "删除" },
        { key: "auth", text: "授权" }
      ]}
      // itemType={"vertical"}
      operationClick={operationClick}
      onRowClick={onRowClick}
      operationTypeProps={{ maxCount: 1 }}
    />

  </div>
}

export default Demo1;
```
