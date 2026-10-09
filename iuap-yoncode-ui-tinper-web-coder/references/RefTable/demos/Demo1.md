---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 单选列表参照
value和onChange作为受控组件，需要传入数组

```js
import React, { useState } from 'react';
import { Tag , ConfigProvider} from '@tinper/next-ui';
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
const { mockData, targetKeys: targetKeysMock } = getMockData(0, 50);

function Demo1 () {
  const [targetKeys, setTargetKeys] = useState([mockData[0]]);
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  })
  const [dataSource, setDataSource] = useState(mockData.slice(0, 20));

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

  const onChange = (current, pageSize) => {
    setPageInfo({
      ...pageInfo,
      current,
      pageSize
    })
    setDataSource(mockData.slice((current - 1) * pageSize, (current) * pageSize))
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
  const onValueChange = (value) => {
    setTargetKeys(value)
  }

  return <div style = {{ height: "200px" }}>
    <ConfigProvider >
      <RefTable
          rowKey={"key"}
          title="授权"
          columns={tableColumns}
          data={dataSource}
          value={targetKeys}
          onChange={onValueChange}
          onSearch={onSearch}
          onSearchChange={onSearch}
          filterOption={filterOption} // 拆成左右两个
          pagination={{
            ...pageInfo,
            onChange
          }}

          allowClear
          fieldNames={{ label: "title" }}
        />
    </ConfigProvider>
    
    <span>
    值：{JSON.stringify(targetKeys)}
    </span>

  </div>
}
export default Demo1;
```
