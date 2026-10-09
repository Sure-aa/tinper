---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 作为表单项使用
作为表单项使用，且后端分页，value接受值，onChange抛出值；右侧列推荐只展示唯一标识和名称（即fieldNames对应的字段）

```js
import React, { useState, useRef } from 'react';
import { Tag, Button, Form, ConfigProvider } from '@tinper/next-ui';
import { RefTable, DataForm } from 'tne-tinpernextpro-fe';
import { useMemo } from 'react';
function getMockData (start, end) {
  const mockData = [];
  const targetKeys = [];
  for (let i = start; i < end; i++) {
    const item = {
      key: i.toString(),
      title: `content${i + 1}`,
      tag: `tag-${i + 1}`,
      description: `description of content${i + 1}`,
      disabled: i % 3 < 1,
      chosen: Math.random() * 2 > 1
    };
    mockData.push(item);
    if (item.chosen) { targetKeys.push(item.key); }
  }
  return { mockData, targetKeys };
}

const { mockData, targetKeys: targetKeysInner } = getMockData(0, 50);

function Demo1 () {
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  })
  const formRef = useRef();
  const [dataSource, setDataSource] = useState(mockData.slice(0, 20));
  const [values, setValues] = useState({});

  const tableColumns = [
    {
      dataIndex: 'title',
      title: 'Name',
      width: 100
    },
    {
      dataIndex: 'tag',
      title: 'Tag',
      width: 100,
      render: (tag) => <Tag>{tag}</Tag>
    },
    {
      dataIndex: 'description',
      title: 'Description'
    }
  ];

  //

  const filterOption = (text, item, direction) => {
    return item.title.indexOf(text) > -1;
  }

  const onSearch = (text) => {
    const newData = mockData.filter(item => {
      return item.title.indexOf(text) > -1;
    })
    setDataSource(newData)
    setPageInfo({
      ...pageInfo,
      current: 1,
      total: newData.length
    })
  }
  const onChange = (current, pageSize) => {
    setPageInfo({
      ...pageInfo,
      current,
      pageSize
    })
    setDataSource(mockData.slice((current - 1) * pageSize, (current) * pageSize))
  }

  const submit = async () => {
    const values = await formRef.current.validateFields();
    setValues(values);
    console.log(values, "values");
  }

  const formItemLayout = {
    labelCol: {
      xs: { span: 4 },
      sm: { span: 4 }
    },
    wrapperCol: {
      xs: { span: 8 },
      sm: { span: 8 }
    }
  };

  return <div style = {{ height: "200px" }}>
    <ConfigProvider>
    <DataForm ref={formRef}>
      <DataForm.Item
        label="选择数据源"
        name="source"
        inputType="custom"
      >
        <RefTable
          rowKey={"key"}
          title="授权"
          labelInValue={true}
          columns={tableColumns}
          data={dataSource}
          showSelectAll={false}
          onSearch={onSearch}
          pagination={{
            ...pageInfo,
            onChange
          }}
          onSearchChange={onSearch}
          filterOption={filterOption}
          allowClear
          fieldNames={{ label: "title" }}
          type="checkbox"
        />
      </DataForm.Item>
    </DataForm>
    {/* <Form ref={formRef} {...formItemLayout}>
      <Form.Item
        label="选择数据源"
        name="source"

      >
        <RefTable
          rowKey={"key"}
          title="授权"
          labelInValue={true}
          columns={tableColumns}
          data={dataSource}
          showSelectAll={false}
          onSearch={onSearch}
          pagination={{
            ...pageInfo,
            onChange
          }}
          onSearchChange={onSearch}
          filterOption={filterOption}
          allowClear
          fieldNames={{ label: "title" }}
          type="checkbox"
        />
      </Form.Item>
    </Form> */}

    <Button onClick={submit}>提交</Button>
    </ConfigProvider>
    <p>值： {JSON.stringify(values)}</p>

  </div>
}
export default Demo1;
```
