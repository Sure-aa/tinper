---
tags:
  - TinperNextPro
  - GroupCascader组件
---
# GroupCascader 级联分组

## 懒加载搜索
懒加载搜索（注：懒加载搜索，搜索的结果不是从options里的数据进行搜索，是从新调用的接口拿到的新数据，这个数据和options没关联）。

```js
import React from 'react';
import { GroupCascader } from 'tne-tinpernextpro-fe';

const optionLists = [
  {
    value: 'zhejiang',
    label: '浙江',
    isLeaf: false,
    groupTopKey: 'abcd',
    groupContentKey: 'c',
    children: [
      {
        value: 'hangzhou',
        label: '杭州',
        isLeaf: false,
        groupTopKey: 'abcd',
        groupContentKey: 'c'
      }
    ]
  },
  {
    value: 'jiangsu',
    label: '江苏',
    isLeaf: false,
    groupTopKey: 'wxyz',
    groupContentKey: 'w',
  },
];
const optionLists1 = [
  {
    value: 'guangdong',
    label: '广东',
    isLeaf: false,
    groupTopKey: 'abcd',
    groupContentKey: 'c'
  },
  {
    value: 'xian',
    label: '西安',
    isLeaf: false,
    groupTopKey: 'wxyz',
    groupContentKey: 'w',
  },
  {
    value: 'hunan',
    label: '湖南',
    isLeaf: false,
    groupTopKey: 'wxyz',
    groupContentKey: 'w',
  },
];
const optionList = [
  {
    value: 'jczj',
    label: '基础组件',
    isLeaf: false,
  },
  {
    value: 'yyzj',
    label: '应用组件',
    isLeaf: false,
  },
]

const demo3 = () => {
  const [options, setOptions] = React.useState(optionList);
  const [searchValue, setSearchValue] = React.useState(optionLists);

  // const [value, setValue] = React.useState([{
  //         value: 'zhejiang',
  //         label: '浙江',
  //         isLeaf: false,
  //         groupTopKey: 'abcd',
  //         groupContentKey: 'c'
  //     },
  //     {
  //         value: 'hangzhou',
  //         label: '杭州',
  //         isLeaf: false,
  //         groupTopKey: 'abcd',
  //         groupContentKey: 'c'
  //     }
  // ]);
  const [value, setValue] = React.useState([{ value: 'jczj', label: '基础组件' }, { value: 'dh', label: '导航' }, { value: 'bq', label: '标签' }])

  const onChange = (value, selectedOptions) => {
    console.log(value, selectedOptions);
    setValue(selectedOptions)
  };

  const onSearch = (val1, val2) => {
    setSearchValue([]) // 每次搜索前需清空searchValue内的值保证获取的相同的值能展示在面板内
    // setTimeout(() => {
    //   this.setState({
    //     searchValue: [val1]
    //   })
    // }, 500)
    if (val1 == '') {
      //   this.setState({
      //     searchValue: []
      //   })
      setTimeout(() => {
        setSearchValue([])
      }, 600)
    } else {
      setTimeout(() => {
        // this.setState({
        //   searchValue: [
        //     {name: '基础组件/导航/标签', value: ['jczj', 'dh', 'bq'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '标签', value: 'bq'}]},
        //     {name: '基础组件/导航/面包屑', value: ['jczj', 'dh', 'mbx'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '面包屑', value: 'mbx'}]},
        //     {name: '基础组件/导航/标签1', value: ['jczj', 'dh', 'bq1'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '标签1', value: 'bq1'}]},
        //   ]
        // })
        setSearchValue([
          { name: '基础组件/导航/标签', value: ['jczj', 'dh', 'bq'], path: [{ label: '基础组件', value: 'jczj', children: [{ label: '导航', value: 'dh', children: [{ label: '标签', value: 'bq' }] }] }, { label: '导航', value: 'dh', children: [{ label: '标签', value: 'bq' }] }, { label: '标签', value: 'bq' }] },
          { name: '基础组件/导航/面包屑', value: ['jczj', 'dh', 'mbx'], path: [{ label: '基础组件', value: 'jczj', children: [{ label: '导航', value: 'dh', children: [{ label: '面包屑', value: 'mbx' }] }] }, { label: '导航', value: 'dh', children: [{ label: '面包屑', value: 'mbx' }] }, { label: '面包屑', value: 'mbx' }] },
          { name: '基础组件/导航/标签1', value: ['jczj', 'dh', 'bq1'], path: [{ label: '基础组件', value: 'jczj', children: [{ label: '导航', value: 'dh', children: [{ label: '标签1', value: 'bq1' }] }] }, { label: '导航', value: 'dh', children: [{ label: '标签1', value: 'bq1' }] }, { label: '标签1', value: 'bq1' }] },
        ])
      }, 500)
      setValue(val1)
    }
  }

  const displayRender = (label) => {
    console.log('sdfsdfsdfsdf', label)
  }

  const onClick = () => {
    // console.log('触发了吗')
    // setOptions(optionLists1)
  }

  const loadData = (selectedOptions, callback) => {
    const targetOption = selectedOptions[selectedOptions.length - 1];
    targetOption.loading = true;

    // load options lazily
    setTimeout(() => {
      targetOption.loading = false;
      targetOption.children = [
        {
          label: `${targetOption.label} Dynamic 1`,
          value: 'dynamic1',
          groupTopKey: 'efgh',
          groupContentKey: 'e'
        },
        {
          label: `${targetOption.label} Dynamic 2`,
          value: 'dynamic2',
          groupTopKey: 'ijkl',
          groupContentKey: 'k',
        },
      ];
      setOptions([...options]);
      callback(targetOption)
    }, 1000);
  };
  return (
    <div onClick={onClick}>
      {/* <GroupCascader value={value} options={options} loadData={loadData} onChange={onChange} onSearch={onSearch} searchValue={searchValue} loadDataFlag={true} showSearch={true}></GroupCascader> */}
      <GroupCascader
        options={options}
        value={value}
        loadData={loadData}
        onChange={onChange}
        onSearch={onSearch}
        searchValue={searchValue}
        loadDataFlag={true}
        showSearch={true}
      />
    </div>

  )
}

export default demo3;
```
