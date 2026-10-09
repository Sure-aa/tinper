---
tags:
  - TinperNextPro
  - GroupCascader组件
---
# GroupCascader 级联分组

## 默认显示第二个页签内容
添加tabsItems属性，默认显示第二个页签项内容。

```js
import React from 'react';
import { GroupCascader } from 'tne-tinpernextpro-fe';
import { jsonData } from './data'

const tabsItems = [
  {
    tab: '江苏省', // 数组第一项的tab对应默认显示两个页签中，第一个页签的头部信息
    key: '1', // 数组第一项的key，可以随便写
    content: jsonData, // 数组第一项的content，可以是整个options，能保证页签第一项内容（比如：第一个页签内容为全部国家，第二个页签为国家对应的省）
  }, {
    tab: '请选择', // 数组第二项的tab对应两个页签中的第二个页签头部（默认显示到第二个页签此时还没选择具体项，所以给值‘请选择’。注：多语需要自行翻译）
    key: '1001Z01000000000SGLN', // 数组第二项的key，对应第一项的tab（‘江苏省’）在options内的value值
    content: jsonData.filter((item) => item.id === '1001Z01000000000SGLN')[0].children // 数组第二项的content，为数组第一项的tab（‘江苏省’）在options内的children
  }
]
const example4 = () => {
  return (
    <GroupCascader
      options={jsonData}
      fieldNames={{ label: 'name', value: 'id' }}
      showSearch={true}
      tabsItems={tabsItems}
    />
  )
}

export default example4;
```
