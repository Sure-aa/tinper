---
tags:
  - TinperNextPro
  - RefTable组件
---
# RefTable 列表参照

## 扩展自定义Header，查询区，以及footer区域
需要自定义dom时可扩展

```js
import React, { useState } from 'react';
import { Button, Tag, ConfigProvider } from '@tinper/next-ui';
import { RefTable, SearchForm } from 'tne-tinpernextpro-fe';
function getMockData(start, end) {
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
    if (item.chosen) {
      targetKeys.push(item.key);
    }
  }
  return { mockData, targetKeys };
}
const { mockData, targetKeys: mocktargetKeys } = getMockData(0, 50);

function Demo1() {
  const [targetKeys, setTargetKeys] = useState([]);
  const [targetData, setTargetData] = useState([
    {
      key: '0',
      title: 'content1',
      tag: 'tag-1',
      description: 'description of content1'
    }
  ]);
  const [pageInfo, setPageInfo] = useState({
    current: 1,
    pageSize: 20,
    total: mockData.length
  });
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
  };

  const onChange = (current, pageSize) => {
    setPageInfo({
      ...pageInfo,
      current,
      pageSize
    });
    setDataSource(mockData.slice((current - 1) * pageSize, current * pageSize));
  };

  const onSearch = (text) => {
    console.log(refs.current.getTableInstance(), 'refs.current.getTableInstance()');
    refs.current.getTableInstance().changeSelectionFilter(false);
    refs.current.getTableInstance().clearSelectedRowKeys([]);
  };

  const onValuesChange = (values, data) => {
    debugger;
    setTargetData(values);
  };

  return (
    <div style={{ height: '200px' }}>
      <RefTable
        rowKey={'key'}
        title={
          <>
            <span>授权</span>
            <Button>自定义按钮</Button>
          </>
        }
        // readOnly
        ref={refs}
        columns={tableColumns}
        data={dataSource}
        onOk={onValuesChange}
        // onChange={onValuesChange}
        value={targetData}
        onSearch={onSearch}
        onSearchChange={onSearch}
        filterOption={filterOption} // 拆成左右两个
        type={'checkbox'}
        fieldNames={{ label: 'title' }}
        pagination={{
          ...pageInfo,
          onChange
        }}
        renderToolBar={(searchDom) => {
          return (
            <div
              dir="rtl"
              style={{
                width: '100%',
                display: 'flex',
                alignItems: 'center',
                justifyContent: 'space-between',
                padding: 8
              }}
            >
              {searchDom}
              <Button>自定义</Button>
            </div>
          );
        }}
        allowClear
        searchContent={
          <SearchForm onSearch={onSearch}>
            <SearchForm.Item inputType="input" name="name" label="关键字" />
            <SearchForm.Item inputType="input" name="name1" label="关键字1" />
            <SearchForm.Item inputType="input" name="name2" label="关键字2" />
          </SearchForm>
        }
        renderFooter={(footer) => {
          return (
            <>
              {footer}
              <Button>自定义</Button>
            </>
          );
        }}
      />
    </div>
  );
}
export default Demo1;
```
