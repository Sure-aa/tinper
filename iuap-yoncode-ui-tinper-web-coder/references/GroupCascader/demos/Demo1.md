---
tags:
  - TinperNextPro
  - GroupCascader组件
---
# GroupCascader 级联分组

## 基础级联分组
基本级联分组(本示例只在北京市设置了分组)。

```js
import React from 'react';
import { GroupCascader } from 'tne-tinpernextpro-fe';
import { jsonData } from './data'

const options = [{
  label: '闲散组件',
  value: 'xsbg',
  groupTopKey: 'abcd',
  groupContentKey: 'c',
  isGroupNum: 15,
}, {
  label: '应用组件',
  value: 'yyzj',
  groupTopKey: 'wxyz',
  groupContentKey: 'w',
  isGroupNum: 15,
  children: [{
    label: '参照',
    value: 'ref',
    groupTopKey: 'abcd',
    groupContentKey: 'a',
    isGroupNum: 15,
    children: [{
      label: '树参照',
      value: 'reftree',
      groupTopKey: 'abcd',
      groupContentKey: 'a',
      isGroupNum: 15,
    }, {
      label: '表参照',
      value: 'reftable',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '穿梭参照',
      value: 'reftransfer',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }]
  }]
}, {
  label: '基础组件',
  value: 'jczj',
  groupTopKey: 'abcd',
  groupContentKey: 'a',
  isGroupNum: 15,
  children: [{
    label: '导航',
    value: 'dh',
    groupTopKey: 'abcd',
    groupContentKey: 'd',
    isGroupNum: 15,
    children: [{
      label: '面包屑',
      value: 'mbx',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '分页',
      value: 'fy',
      groupTopKey: 'efgh',
      groupContentKey: 'f',
      isGroupNum: 15,
    }, {
      label: '标签',
      value: 'bq',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '菜单',
      value: 'cd',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }, {
      label: '面包屑1',
      value: 'mbx1',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '分页1',
      value: 'fy1',
      groupTopKey: 'efgh',
      groupContentKey: 'f',
      isGroupNum: 15,
    }, {
      label: '标签1',
      value: 'bq1',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '菜单1',
      value: 'cd1',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }, {
      label: '面包屑2',
      value: 'mbx2',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '分页2',
      value: 'fy2',
      groupTopKey: 'efgh',
      groupContentKey: 'f',
      isGroupNum: 15,
    }, {
      label: '标签2',
      value: 'bq2',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '菜单2',
      value: 'cd2',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }, {
      label: '面包屑3',
      value: 'mbx3',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '分页3',
      value: 'fy3',
      groupTopKey: 'efgh',
      groupContentKey: 'f',
      isGroupNum: 15,
    }, {
      label: '标签3',
      value: 'bq3',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '菜单3',
      value: 'cd3',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }, {
      label: '面包屑4',
      value: 'mbx4',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '分页4',
      value: 'fy4',
      groupTopKey: 'efgh',
      groupContentKey: 'f',
      isGroupNum: 15,
    }, {
      label: '标签4',
      value: 'bq4',
      groupTopKey: 'abcd',
      groupContentKey: 'b',
      isGroupNum: 15,
    }, {
      label: '菜单4',
      value: 'cd4',
      groupTopKey: 'abcd',
      groupContentKey: 'c',
      isGroupNum: 15,
    }]
  }, {
    label: '反馈',
    value: 'fk',
    groupTopKey: 'efgh',
    groupContentKey: 'f',
    isGroupNum: 15,
    children: [{
      label: '模态框',
      value: 'mtk',
      groupTopKey: 'jklm',
      groupContentKey: 'm',
      isGroupNum: 15,
    }, {
      label: '通知',
      value: 'tz',
      groupTopKey: 'stwx',
      groupContentKey: 't',
      isGroupNum: 15,
    }]
  },
  {
    label: '表单',
    value: 'bd',
    groupTopKey: 'abcd',
    groupContentKey: 'b',
    isGroupNum: 15,
  }]
}, {
  label: '业务组件',
  value: 'cpbg',
  groupTopKey: 'abcd',
  groupContentKey: 'a',
  isGroupNum: 15,
}
];

// const example1 = () => {
//   onSearch = (val1, val2) => {
//     setTimeout(() => {
//       this.setState({
//         searchValue: [val1]
//       })
//     }, 500)
//   }
//   return (
//     <GroupCascader options={options} onSearch={this.onSearch}></GroupCascader>
//   )
// }
// class example1 extends React.Component {
//   constructor(props) {
//     super(props)
//     this.state = {
//       searchValue: []
//     }
//   }
//   onSearch = (val1, val2) => {
//     // setTimeout(() => {
//     //   this.setState({
//     //     searchValue: [val1]
//     //   })
//     // }, 500)
//     // console.log('demo内的onsearch', val1)
//     // if (val1 == '') {
//     //   // this.setState({
//     //   //   searchValue: []
//     //   // })
//     //   setTimeout(() => {
//     //     this.setState({
//     //       searchValue: []
//     //     })
//     //   }, 600)
//     // } else {
//     //   setTimeout(() => {
//     //     this.setState({
//     //       searchValue: [
//     //         {name: '基础组件/导航/标签', value: ['jczj', 'dh', 'bq'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '标签', value: 'bq'}]},
//     //         {name: '基础组件/导航/面包屑', value: ['jczj', 'dh', 'mbx'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '面包屑', value: 'mbx'}]},
//     //         {name: '基础组件/导航/标签1', value: ['jczj', 'dh', 'bq1'], path: [{label: '基础组件', value: 'jczj'}, {label: '导航', value: 'dh'}, {label: '标签1', value: 'bq1'}]},
//     //       ]
//     //     })
//     //   }, 500)

//     // }

//   }
//   render() {
//     return (
//       <div>
//         {/* <div style={{height: '200px'}}>上站位</div> */}
//         <GroupCascader options={jsonData} fieldNames={{ label: 'name', value: 'id' }} onSearch={this.onSearch} showSearch={true}></GroupCascader>
//         {/* <div style={{height: '800px', background: 'red'}}>下站位</div> */}
//       </div>

//     )
//   }
// }
const example1 = () => {
  return (
    <GroupCascader
      options={jsonData}
      fieldNames={{ label: 'name', value: 'id' }}
      showSearch={true}
    />
  )
}

export default example1;
```
