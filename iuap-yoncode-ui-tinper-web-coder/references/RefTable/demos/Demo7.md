---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 参照只读
支持只读

```js
import React, { useState } from 'react';
import { Tag, ConfigProvider } from '@tinper/next-ui';
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
const { mockData, targetKeys: targetKeysInner } = getMockData(0, 50);

function Demo1 () {
  // const [targetKeys, setTargetKeys] = useState(targetKeysInner);
  const [targetData, setTargetData] = useState([mockData[40]]);
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  })
  const [dataSource, setDataSource] = useState(mockData);

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
  const onValuesChange = (data) => {
    setTargetData(data)
  }

  // todo 去掉全部选择按钮
  return <div style = {{ minHeight: "200px" }}>
    <ConfigProvider>
      <p>多选参照只读</p>
      <RefTable
          rowKey={"key"}
          title="授权"
          readOnly
          columns={tableColumns}
          data={dataSource}
          onChange={onValuesChange}
          value={mockData.slice(2,4)}
          onSearch={onSearch}
          onSearchChange={onSearch}
          filterOption={filterOption} // 拆成左右两个
          allowClear
          fieldNames={{ label: "title" }}
          maxTagCount={5}
          type="checkbox"

        />
        <p>单选参照只读</p>
          <RefTable
            rowKey={"key"}
            title="授权"
          readOnly

            columns={tableColumns}
            data={dataSource}
            value={targetData}

            onSearch={onSearch}
            onSearchChange={onSearch}
            filterOption={filterOption} // 拆成左右两个
            pagination={{
              ...pageInfo,

            }}
  
            allowClear
            fieldNames={{ label: "title" }}
          />
    </ConfigProvider>
    

    <>
    值：{JSON.stringify(targetData)}
    </>

  </div>
}
export default Demo1;
```
