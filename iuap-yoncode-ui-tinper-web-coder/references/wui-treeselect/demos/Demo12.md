---
tags:
  - TinperNext
  - treeselect组件
---
# 树选择 TreeSelect

## treeSelect readOnly只读态

readOnly只读态 单选 和 多选模式；自定义treeNode节点需要设置selectable=false。

```tsx
import {TreeSelect} from '@tinper/next-ui';
import React, {Component} from 'react';

const {TreeNode} = TreeSelect;

const treeData: any[] = [{
    title: '0-0',
    value: '0-0',
    key: '0-0',
    children: [{
        title: '0-0-1',
        value: '0-0-1',
        key: '0-0-1',
    }, {
        title: '0-0-2',
        value: '0-0-2',
        key: '0-0-2',
    }, {
        title: '0-0-3',
        value: '0-0-3',
        key: '0-0-3',
    }, {
        title: '0-0-4',
        value: '0-0-4',
        key: '0-0-4',
    }, {
        title: '0-0-5',
        value: '0-0-5',
        key: '0-0-5',
    }],
}, {
    title: '0-1',
    value: '0-1',
    key: '0-1',
}];

class Demo12 extends Component {
    state = {
        readOnly: true
    }


    render() {
	    return (
	        <div>
	            <h4>单选且自定义节点</h4>
	            <TreeSelect
	                bordered='bottom'
	                style={{width: 300}}
	                value={'leaf1'}
	                placeholder="请选择"
	                allowClear
	                treeDefaultExpandAll
	                readOnly={true}
	            >
	                <TreeNode selectable={false} value="parent 1" title="用友网络股份有限公司" key="0-1">
	                    <TreeNode selectable={false} value="parent 1-0" title="用友网络股份有限公司1-0" key="0-1-1">
	                        <TreeNode selectable={false} value="leaf1" title="用友网络股份有限公司leaf" key="random"/>
	                        <TreeNode selectable={false} value="leaf2" title="用友网络股份有限公司leaf" key="random1"/>
	                    </TreeNode>
	                    <TreeNode selectable={false} value="parent 1-1" title="用友网络股份有限公司" key="random2">
	                        <TreeNode selectable={false} value="sss" title="用友网络股份有限公司" key="random3"/>
	                    </TreeNode>
	                </TreeNode>
	            </TreeSelect>
	            <h4>单选treeData 模式</h4>
	            <TreeSelect
	                autoClearSearchValue={false}
	                style={{width: 300}}
	                value={'0-0-1'}
	                dropdownStyle={{maxHeight: 400, overflow: 'auto'}}
	                treeData={treeData}
	                treeDefaultExpandAll
	                showSearch={!this.state.readOnly}
	                readOnly={this.state.readOnly}
	            />
	            <h4>多选treeData 模式</h4>
	            <TreeSelect
	                autoClearSearchValue={false}
	                style={{width: 300}}
	                value={['0-0-1', '0-0-2', '0-0-3', '0-0-5']}
	                dropdownStyle={{maxHeight: 400, overflow: 'auto'}}
	                multiple
	                maxTagCount={"responsive"}
	                treeData={treeData}
	                treeDefaultExpandAll
	                readOnly={true}
	            />
	        </div>
	    )
    }
}

export default Demo12;
```
