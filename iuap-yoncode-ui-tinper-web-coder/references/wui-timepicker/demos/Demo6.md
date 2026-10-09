---
tags:
  - TinperNext
  - timepicker组件
---
# 时间 TimePicker

## 时间间隔

设置时分秒间隔。

```tsx
import {TimePicker} from '@tinper/next-ui'
import React, {Component} from 'react'

class Demo6 extends Component {
    render() {
        return (
            <div>
                <TimePicker
                    placeholder='选择时间'
                    hourStep={3}
                    minuteStep={4}
                    secondStep={5}
                />
            </div>
        )
    }
}

export default Demo6
```
