---
tags:
  - TinperNextPro
  - GroupCascader组件
---
# GroupCascader 级联分组

## 基础级联分组2
基本级联分组2。

```js
import React from 'react';
import { GroupCascader } from 'tne-tinpernextpro-fe';

const optionLists = [
  {
    value: 'zhejiang',
    label: 'Zhejiang',
    isLeaf: false,
    groupTopKey: 'abcd',
    groupContentKey: 'c'
  },
  {
    value: 'jiangsu',
    label: 'Jiangsu',
    isLeaf: false,
    groupTopKey: 'wxyz',
    groupContentKey: 'w',
  },
];

const example1 = () => {
  const [options, setOptions] = React.useState(optionLists);

  const onChange = (value, selectedOptions) => {
    console.log(value, selectedOptions);
  };

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
    <GroupCascader
      options={options}
      loadData={loadData}
      onChange={onChange}
    />
  )
}

export default example1;
```
