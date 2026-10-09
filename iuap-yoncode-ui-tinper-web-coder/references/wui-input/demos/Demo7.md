---
tags:
  - TinperNext
  - input组件
---
# 输入框 Input

## 不可用状态

添加 disabled 属性即可让输入框处于不可用状态

```tsx
import {Input} from '@tinper/next-ui'
import React, {Component} from 'react'

export default class Demo1 extends Component {
    render() {
        return (
            <div className='demo7'>
                <Input
                    disabled
                    value='test'
                    style={{marginTop: '10px', width: '200px'}}
                />
            </div>
        )
    }
}
```
