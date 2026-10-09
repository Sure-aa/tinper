---
tags:
  - TinperNext
  - timepicker组件
---
# 时间 TimePicker

## 浏览态

设置 browser=true

```tsx
import {TimePicker} from '@tinper/next-ui'
import moment from 'moment'
import React, {Component} from 'react'

class Demo10 extends Component {

    render() {
        const format = 'h:mm a'
        const now = moment().hour(0).minute(0)
        return (
            <div>
                <TimePicker
                    fieldid='dem11_fieldid'
                    browser
                    format={format}
                    value={now}
                />
            </div>
        )
    }
}

export default Demo10
```
