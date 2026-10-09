---
tags:
  - TinperNext
  - datepicker组件
---
# 日期 DatePicker

## 浏览态

设置browser属性，只显示文本，不渲染输入框

```tsx
import { Col, ConfigProvider, DatePicker, Row } from '@tinper/next-ui'
import moment, { Moment } from 'moment'
import React, { Component } from 'react'

const {RangePicker, HalfYearPicker} = DatePicker

interface DemoState {
    value: Moment | null
    halfYear: Moment | string | null
    year: Moment | null
    rangeValue: [Moment | null, Moment | null] | null
}

class Demo32 extends Component<{}, DemoState> {
    constructor(props: {}) {
        super(props)
        this.state = {
            value: null,
            // halfYear: '3333 FH',
            halfYear: moment().add(10, 'M'),
            year: null,
            rangeValue: [moment(), moment().add(10, 'M')]
        }
    }

    render() {
        return (
            <ConfigProvider>
                <div>
                    <Row gutter={[10, 10]}>
                        <Col md={12}>
                            <DatePicker
                                defaultValue='2036-04-23'
                                format='YYYY-MM-DD'
                                placeholder='选择日期'
                                showToday
                                onChange={this.onChange}
                                browser
							    fieldid='xxxaaa'
                                hiddenFields={['MM', 'ww']}
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                showTime
                                format='YYYYMMDD HHmmss'
                                placeholder='YYYYMMDD HHmmss'
                                browser
                                value={moment()}
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                browser
                                value={moment()}
                                showTime={{defaultValue: '00:00:00'}}
                                format={[
                                    'YYYY-MM-DD HH:mm:ss',
                                    'YYYY/MM/DD HH:mm:ss',
                                    'YYYY.MM.DD HH:mm:ss',
                                    'YYYYMMDD HH:mm:ss',
                                    'MM-DD-YYYY HH:mm:ss',
                                    'MM/DD/YYYY HH:mm:ss',
                                    'DD.MM.YYYY HH:mm:ss'
                                ]}
                                placeholder='选择日期时刻'
                                hiddenFields={['MM', 'ww']}
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                picker='week'
                                placeholder='选择周'
                                browser
                                value={moment()}
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                picker='month'
                                format='YYYY-MM'
                                placeholder='选择年月'
                                allowClear={false}
                                autoFocus
                                value={this.state.value}
                                browser
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                picker='quarter'
                                locale={{locale: 'zh-cn', quarterFormat: '第Q季度'}}
                                format='YYYY-Q季度'
                                placeholder='选择季度'
                                value={this.state.value}
                                browser
                            />
                        </Col>
                        <Col md={12}>
                            <HalfYearPicker
                                browser
                                locale='zh-cn'
                                placeholder='选择半年'
                                value={this.state.halfYear}
                            />
                        </Col>
                        <Col md={12}>
                            <DatePicker
                                picker='year'
                                format='YYYY'
                                placeholder='选择年'
                                value={this.state.year}
                                browser
                            />
                        </Col>
                        <Col md={12}>
                            <RangePicker
                                autoFix
                                value={this.state.rangeValue}
                                placeholder={['开始', '结束']}
                                browser
							    fieldid='xxxaaa'
                                hiddenFields={['MM', 'ww']}
                            />
                        </Col>
                        <Col md={12}>
                            <RangePicker
                                allowClear
                                allowEmpty={[true, true]}
                                bordered="bottom"
                                format="YYYY-MM-DD"
                                picker="date"
                                placeholder={['showToday', 'showToday']}
                                requiredStyle
                                showToday
                                value={this.state.rangeValue}
                                browser
                            />
                        </Col>
                        <Col md={12}>
                            <RangePicker
                                autoFix
                                value={this.state.rangeValue}
                                format='YYYY/MM/DD HH:mm:ss'
                                placeholder={['开始', '结束']}
                                disabled={[true, false]}
                                bordered="bottom"
                                readOnly
                                requiredStyle
                                showTime={{
                                    defaultValue: ['00:00:00', '23:59:59']
                                }}
                                browser
                                separator='至'
                                hiddenFields={['MM', 'ww']}
                            />
                        </Col>
                        <Col md={12}>
                            <RangePicker
                                autoFix
                                picker='halfYear'
                                value={this.state.rangeValue}
                                placeholder={['开始半年', '结束半年']}
                                browser
                            />
                        </Col>
                    </Row>
                </div>
            </ConfigProvider>
        )
    }
}

export default Demo32
```
