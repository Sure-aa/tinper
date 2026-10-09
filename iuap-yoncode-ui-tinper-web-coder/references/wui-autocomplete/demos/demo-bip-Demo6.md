---
tags:
  - TinperNext
  - autocomplete组件
---
# 自动完成 AutoComplete

## 禁用态和浏览态

显示不同状态

```tsx
import {AutoComplete} from '@tinper/next-ui'
import React, {Component} from 'react'

interface DemoState {
    options: string[]
    placeholder: string
}

class Demo6 extends Component<{}, DemoState> {
    constructor(props: {}) {
        super(props)
        this.state = {
            options: ['10000', '10001', '10002', '11000', '12010'],
            placeholder: '查找关键字,请输入1'
        }
    }

    render() {
        let {options, placeholder} = this.state
        return (
            <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
                <div>禁用态</div>
                <AutoComplete options={options} placeholder={placeholder} disabled/>
                <div>只读态</div>
                <AutoComplete options={options} placeholder={placeholder} readOnly/>

            </div>
        )
    }
}

export default Demo6
```
