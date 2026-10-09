---
tags:
  - TinperNextPro
  - TableTransfer组件
---
# TableTransfer 列表穿梭

## 前端分页表格穿梭
受控tagetData使用方式。1. 如果显示全部选择，被选数据来源为分页请求后端，右侧已选区数据来源可通过TargetData受控配置。2.如果后端接口分页想要做数据回显，使用该字段

```js
import React, { useState } from 'react';
import { Tag, ConfigProvider } from '@tinper/next-ui';
import { TableTransfer } from 'tne-tinpernextpro-fe';
function getMockData(start, end) {
  const mockData = [];
  const targetKeys = [];
  const targetData = [];
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
    if (item.chosen) {
      targetKeys.push(item.key);
      targetData.push(item);
    }
  }
  return { mockData, targetKeys, targetData };
}
const { mockData, targetData: targetDataMock } = getMockData(0, 50);

function Demo1() {
  const [targetData, setTargetData] = useState(targetDataMock);
  const [pageInfo, setPageInfo] = useState({
    // current: 1,
    simple: false,
    pageSize: 20,
    total: mockData.length
  });
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
  };

  const onSearch = (text) => {
    const newData = mockData.filter((item) => {
      return item.title.indexOf(text) > -1;
    });
    setDataSource(newData);
    setPageInfo({
      ...pageInfo,
      current: 1,
      total: newData.length
    });
  };
  const onSelectAll = () => {
    setTargetData([...mockData]);
  };
  const onSelectChange = (keys, data) => {
    setTargetData(data);
  };

  return (
    <div style={{ height: '50vh' }}>
      <ConfigProvider>
        <TableTransfer
          rowKey={'key'}
          onSelectChange={onSelectChange}
          leftColumns={tableColumns}
          rightColumns={tableColumns}
          titles={['可选列表', '已选列表']}
          data={dataSource}
          targetData={targetData}
          onSearch={onSearch}
          // onSearchChange={onSearch}
          filterOption={filterOption} // 拆成左右两个
          onSelectAll={onSelectAll}
          rowSelection={{
            getCheckboxProps: (record, index) => {
              return {
                disabled: targetData[0].key === record.key
              };
            }
          }}
          pagination={{
            ...pageInfo
            // onChange
          }}
        />
      </ConfigProvider>
    </div>
  );
}
export default Demo1;
```
