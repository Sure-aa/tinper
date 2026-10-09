---
tags:
  - TinperNext
  - datepicker组件
---
# 日期 DatePicker

## 格式化splitDate方法验证示例

测试用例

```tsx
import { ConfigProvider, DatePicker } from '@tinper/next-ui'
import React, { Component } from 'react'

class Demo30 extends Component {
    render() {
        return (
            <ConfigProvider>
                <div>
                    <DatePicker
                        format='YYYYMM'
                        placeholder='YYYYMM'
                    />
                    <DatePicker
                        format='YYYYMMDD'
                        placeholder='YYYYMMDD'
                    />
                    <DatePicker
                        showTime
                        format='YYYYMMDDHHmmss'
                        placeholder='YYYYMMDDHHmmss'
                    />
                    <DatePicker
                        showTime
                        format='YYYYMMDD HHmmss'
                        placeholder='YYYYMMDD HHmmss'
                    />
                    <DatePicker
                        showTime
                        format='YYYY/MM/DD HH:mm:ss'
                        placeholder='YYYY/MM/DD HH:mm:ss'
                    />
                </div>
            </ConfigProvider>
        )
    }
}

export default Demo30
```
