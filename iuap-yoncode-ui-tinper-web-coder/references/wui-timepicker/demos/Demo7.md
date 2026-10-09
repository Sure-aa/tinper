---
tags:
  - TinperNext
  - timepicker组件
---
# 时间 TimePicker

## 自定义页脚

设置 `renderExtraFooter` 自定义页脚。

```tsx
import {TimePicker} from '@tinper/next-ui'
import moment from 'moment'
import React, {Component} from 'react'
import type {Moment} from 'moment'

class Demo7 extends Component {
    onChange(time: Moment, timeString: string) {
        console.log(time, timeString)
    }

    render() {
        const format = 'h:mm a'
        const now = moment().hour(0).minute(0)
        return (
            <div>
                <TimePicker
                    className='test111'
                    popupClassName='test222'
                    fieldid='demo7_fieldid'
                    format={format}
                    defaultValue={now}
                    placeholder='选择时间'
                    onChange={this.onChange}
                    use12Hours
                    allowClear
                    renderExtraFooter={() => (<>我是额外的页脚</>)}
                />
            </div>
        )
    }
}

export default Demo7
```
