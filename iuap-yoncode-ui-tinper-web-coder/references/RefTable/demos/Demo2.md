---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 多选列表参照
受控tagetData使用方式。1. 如果显示全部选择，被选数据来源为分页请求后端，右侧已选区数据来源可通过TargetData受控配置。2.如果后端接口分页想要做数据回显，使用该字段

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
const { mockData } = getMockData(0, 50);

function Demo1 () {
  const [targetData, setTargetData] = useState([mockData[40]]);
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  })

  const refs = React.useRef();
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
    setSelectedData(mockData.slice((current - 1) * pageSize, (current) * pageSize))
  }

  const onSearch = (text) => {
    const newData = mockData.filter(item => {
      return item.title.indexOf(text) > -1;
    })
    // refs.current.getTableInstance().changeSelectionFilter(false)
    setDataSource(newData)
    setPageInfo({
      ...pageInfo,
      current: 1,
      total: newData.length
    })
  }
  const onSelectAll = () => {
    setTargetData(mockData)
  }
  const onValsChange = (data) => {
    setTargetData(data)
  }

  return <div style = {{ minHeight: "200px" }}>
    <ConfigProvider >

      <RefTable
        rowKey={"key"}
        title="授权"
        columns={tableColumns}
        data={dataSource}
        value={targetData}
        onChange={onValsChange}
        // onSearch={onSearch}
        // onSearchChange={onSearch}
        filterOption={filterOption} // 拆成左右两个
        onSelectAll={onSelectAll}
        pagination={{
          ...pageInfo,
          onChange
        }}
        ref={refs}
        type={"checkbox"}
        allowClear
        fieldNames={{ label: "title" }}
        maxTagCount={5}
      />
    </ConfigProvider>

    <>
    值：{JSON.stringify(targetData)}
    </>

  </div>
}
export default Demo1;
```
