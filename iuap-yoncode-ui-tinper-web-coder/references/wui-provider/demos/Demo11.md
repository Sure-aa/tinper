---
tags:
  - TinperNext
  - provider组件
---
# 全局化配置 ConfigProvider

## 全局配置首选项格式

支持全局或局部配置日期/时间组件格式并转换为输入框、面板配置

```tsx
import { ConfigProvider, DatePicker } from '@tinper/next-ui'
import React, { Component } from 'react'

const {MonthPicker, RangePicker, YearPicker, WeekPicker, HalfYearPicker} = DatePicker

class Demo11 extends Component<{}, any> {
    constructor(props) {
        super(props)
        this.state = {
            value: null
        }
    }
    handleChange = (value: any, dateString: string) => {
        this.setState({
            value: dateString
        })
        console.log('111--------', value, dateString)
    }

    render() {
        // 配置dataFormat并的三个可选参数dateTimeFormat, dateFormat, timeFormat三个日期时间格式
        // ConfigProvider.config({
        //     dataFormat: {dateTimeFormat: 'yyyy-MM-dd hh:mm:ss tt', dateFormat: 'YYYY.MM.DD', timeFormat: 'hh:mm a'}
        // })

        return (
            <div className='demo1'>
                <ConfigProvider>
                    <DatePicker placeholder='日期时间' enableTimezone showNow showTime value={this.state.value} onChange={this.handleChange} />

                    <RangePicker enableTimezone picker='date' placeholder='日期' onChange={this.handleChange} />

                    <HalfYearPicker enableTimezone onChange={this.handleChange} />

                    年历：
                    <YearPicker />
                    月历：
                    <MonthPicker />
                    周历：
                    <WeekPicker />
                </ConfigProvider>
            </div>
        )
    }
}

export default Demo11
```
