---
tags:
  - TinperNext
  - skeleton组件
---
# 骨架屏 Skeleton

## Skeleton复杂的组合

多种属性的使用

```tsx
import {Skeleton} from '@tinper/next-ui'
import React, {Component} from 'react'

class Demo extends Component {
    render() {
        return (
            <Skeleton avatar title paragraph={{rows: 4, width: ['50%', '60%']}}/>
        )
    }
}

export default Demo;
```
