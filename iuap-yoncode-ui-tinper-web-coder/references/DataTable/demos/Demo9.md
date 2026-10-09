---
tags:
  - TinperNextPro
  - DataTable组件
---
# DataTable 数据表格

## 全局tabs标准布案例
继承于TinperNext-Table组件。

```tsx
import React, { useState, useRef, useMemo, useCallback } from "react";
import { Button, Space, Tabs } from '@tinper/next-ui';
import { services } from './mockData';
import { DataTable, SearchForm } from 'tne-tinpernextpro-fe';
import './Demo9.less';
function Demo8 () {
  // 输出模拟数据
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);

  const [group, setGroup] = useState(1);
  const [activeKey, setActiveKey] = useState("tab1");

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
      min={100}
      max={200}
    />
    <SearchForm.Item htmlFor={false} inputType="search" label="搜索框" name="search" />
    <SearchForm.Item htmlFor={false} inputType="select" label="下拉框" name="select" />
    <SearchForm.Item htmlFor={false} inputType="password" label="密码框" name="password" />
  </SearchForm>), [])

  const renderToolBar = useCallback(() => {

          return <div style={{ width: "100%", textAlign: "right" }}>
            <Space>
              <Button type="primary">新增</Button>

            </Space>
          </div>

  })

  const tabs = [
    {
      key: "tab1",
      tab: "标签1",
      children: <DataTable
        ref={tableRef}
        // searchContent={ searchContent}

        renderToolBar={renderToolBar}
        stripeLine

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
        showModeSwitch={true}

        sort={{ mode: "single", backSource: false, sortFun: sortFunc }}
        pagination={true}
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
    },
    {
      key: "tab2",
      tab: "标签2",
      children: <DataTable
        ref={tableRef}
        showModeSwitch={true}
        // searchContent={ searchContent}

        renderToolBar={renderToolBar}

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
        pagination={true}
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
    }
  ]

  const onTabChange = (key: string) => {
    setActiveKey(key)
  }
  return <div style={{ height: '50vh' }}>
    <Tabs className={"tab-demo-wrapper"} type="card" activeKey={activeKey} onChange={onTabChange} defaultActiveKey={"tab1"}>
      {
        tabs.map(item => {
          return <Tabs.TabPane key={item.key} tab={item.tab}>
            {item.children}
          </Tabs.TabPane>
        })
      }
    </Tabs>

  </div>
}

export default Demo8;
```

```less
.tab-demo-wrapper{
  height: 100%;
  overflow-y: hidden;
  .wui-tabs-content{

    height: calc(100% - 36px)!important;
    overflow-y: hidden;
  }
  .wui-tabs-tabpane{
    height:100%;
  }
  .wui-tabs-bar{
    margin-bottom: 0px;
  }
}
```
