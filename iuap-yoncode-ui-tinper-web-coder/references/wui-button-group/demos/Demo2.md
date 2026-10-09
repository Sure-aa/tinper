---
tags:
  - TinperNext
  - buttongroup组件
---
# 按钮组 ButtonGroup

## 垂直排列的按钮组

通过`vertical`属性设置按钮组垂直排列

```tsx
import {Button, ButtonGroup, Icon} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <ButtonGroup vertical>
                <Button colors="primary"><Icon type='uf-navmenu'/></Button>
                <Button colors="info"><Icon type='uf-file'/></Button>
                <Button colors="warning"><Icon type='uf-del'/></Button>
            </ButtonGroup>
        )
    }
}


export default Demo2;
```
