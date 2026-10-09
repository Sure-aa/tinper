---
tags:
  - TinperNext
  - datepicker组件
---
# 日期 DatePicker

## 只读

设置readOnly属性，输入框只读（面板、按钮、快捷键等不可操作选择，面板不显示），设置inputReadOnly属性，输入框只读（面板、按钮、快捷键等可操作选择，面板显示）

```tsx
import { ConfigProvider, DatePicker } from '@tinper/next-ui'
import React, { Component } from 'react'

const { RangePicker } = DatePicker

class Demo31 extends Component {
    render() {
        return (
            <ConfigProvider>
                <div>
                    <DatePicker
                        defaultValue='2036-04-23'
                        readOnly
                    />
                    <DatePicker
                        defaultValue='2036-04-23'
                        inputReadOnly
                    />
                    <RangePicker
                        readOnly
                        value={['2036-04-23', '2036-04-23']}
                    />
                    <RangePicker
                        inputReadOnly
                        value={['2036-04-23', '2036-04-23']}
                    />
                </div>
            </ConfigProvider>
        )
    }
}

export default Demo31
```
