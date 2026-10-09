---
tags:
  - TinperNext
  - tree组件
---
# 树形控件 Tree

## 树checkbox的实心背景样式

设置inverse为true，checkbox的背景色变成主题色填充色，加减符号是白色。

```tsx
import {Tree} from '@tinper/next-ui';
import React, {Component} from 'react';
const TreeNode = Tree.TreeNode

class Demo16 extends Component {
    constructor(props: {}) {
        super(props);
    }
    render() {
        return (
            <Tree
                checkable
                inverse
                defaultExpandAll
                className="myCls"
            >
                <TreeNode title="parent" key="0-0-0">
                    <TreeNode title="leaf1" key="0-0-0-0"/>
                    <TreeNode title="leaf2" key="0-0-0-1"/>
                    <TreeNode title="leaf3" key="0-0-0-2"/>
                </TreeNode>
            </Tree>
        );
    }
}

export default Demo16;
```
