---
tags:
  - TinperNext
  - alert组件
---
# 平面提示 Alert

## 基本样式展示

基本样式展示

```tsx
import {Alert} from '@tinper/next-ui'
import React, {Component} from 'react'

class Demo1 extends Component {
    render() {
        return (
            <Alert id='demo1-id' fieldid='demo1-fieldid' type='danger' showIcon className='my-className'>
                这是一条很长的信息提示
            </Alert>
        )
    }
}

export default Demo1
```
