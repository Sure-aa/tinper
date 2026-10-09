---
tags:
  - TinperNext
  - inputnumber组件
---
# 数字框 InputNumber

## onStep 属性

点击上下按钮时回调函数

```tsx
import {InputNumber} from '@tinper/next-ui'
import React, {Component} from 'react'

class Demo14 extends Component {
    handleStep(value: number, {offset, type}: {offset: number; type: "up" | "down"}) {
        console.log(value, offset, type)
    }

    render() {
        return (
            <div>
                <InputNumber onStep={this.handleStep} step={5} min={-999999} max={999999}/>
            </div>
        )
    }
}

export default Demo14
```
