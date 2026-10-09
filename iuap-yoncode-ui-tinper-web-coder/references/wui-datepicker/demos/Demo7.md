---
tags:
  - TinperNext
  - datepicker组件
---
# 日期 DatePicker

## 预设日期

可以传入预设的日期快捷选项。

```tsx
import type { DatePickerProps } from '@tinper/next-ui'
import { ConfigProvider, DatePicker, Row } from '@tinper/next-ui'
import moment from 'moment'
import React, { Component } from 'react'

interface DemoState {
    value: DatePickerProps['value']
    activePresetKey: string;
}

moment.locale('zh-cn')

class Demo7 extends Component<{}, DemoState> {
    constructor(props: {}) {
        super(props)
        this.state = {
            value: null,
            activePresetKey: 'today',
        }
    }

    /**
     * @param label 触发快捷日期文本
     * @param value 日期
     * @param key 快捷键的key
     */
    handlePresetChange: DatePickerProps['onPresetChange'] = (label, value, key) => {
        console.log('111----------presetChange', label, value, key)
        this.setState({value, activePresetKey: key})
    }

    handleChange = (value: DatePickerProps['value']) => {
        console.log('111----------value', value)
    }

    render() {
        const {value, activePresetKey} = this.state
        return (
            <Row gutter={[10, 10]}>
                <ConfigProvider>
                    <DatePicker
                        allowClear
                        activePresetKey={activePresetKey}
                        value={value}
                        onPresetChange={this.handlePresetChange}
                        showToday
                        // showTime
                        // use12Hours
                        presets={[
                            {
                                label: '今天',
                                key: 'today',
                                value: moment().startOf('day'),
                            },
                            'tomorrow',
                            {
                                label: '三年后', // 内置值仅传入key即可，自定义值需传入{label, key, value}对象
                                key: 'threeYearsLater',
                                value: moment().startOf('day').add(3, 'y'),
                            },
                        ]}
                    />


                    <DatePicker
                        allowClear
                        onChange={this.handleChange}
                        presets
                    />
                </ConfigProvider>
            </Row>
        )
    }
}

export default Demo7
```
