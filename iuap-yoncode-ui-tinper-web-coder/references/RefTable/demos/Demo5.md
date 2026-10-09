---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 自定义参照触发区域-单选,labelInValue使用
children自定义触发，可更换成按钮

```js
import React, { useState, useRef } from 'react';
import { Button, Tag, ConfigProvider } from '@tinper/next-ui';
import { RefTable } from 'tne-tinpernextpro-fe';
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
const { mockData, targetKeys: mocktargetKeys } = getMockData(0, 50);

function Demo1 () {
  const [targetKeys, setTargetKeys] = useState([]);
  const [targetData, setTargetData] = useState([]);
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  })
  const [dataSource, setDataSource] = useState(mockData);
  const refer = useRef(null);
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
  const onChange = (data) => {
    setTargetKeys(data)
    console.log("keys", data)
  }

  const openModal = () => {
    // refer.current.clearSelect()
    refer.current.openModal()
  }

  return <div style = {{ height: "200px" }}>
    <ConfigProvider >
    <RefTable
      ref={refer}
      rowKey={"key"}

      title={<>
        <span>授权</span>
      </>}
      columns={tableColumns}
      data={mockData}
      onSearch={onSearch}
      onSearchChange={onSearch}
      filterOption={filterOption} // 拆成左右两个
      onChange={onChange}
      fieldNames={{ label: "title" }}
      value={targetKeys}
      labelInValue={false}
      type="radio"
    >
      <Button onClick={openModal}>打开参照，选择数据源</Button>

    </RefTable>
    </ConfigProvider>
    <p>
      选中数据：
      {JSON.stringify(targetKeys)}
    </p>
  </div>
}
export default Demo1;
```
