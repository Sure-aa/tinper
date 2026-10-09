---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 时区 - scrollIntoValue 动态滚动

演示多选模式下 scrollIntoValue 的时区转换和动态更新。

```tsx
import {Calendar, Button, Space} from '@tinper/next-ui';
import moment, {Moment} from 'moment';
import React, {Component} from 'react';

interface Demo40State {
    scrollIntoValue: Moment;
    selectedDates: string[];
}

class Demo40 extends Component<{}, Demo40State> {
    state: Demo40State = {
        scrollIntoValue: moment('2023-06-15'),
        selectedDates: []
    };

    onChange = (value: Moment, flag: boolean, valueStrings: string[]) => {
        console.log('onChange - 选中的日期（UTC）:', valueStrings);
        this.setState({selectedDates: valueStrings});
    };

    scrollToDate = (date: string) => {
        this.setState({
            scrollIntoValue: moment(date)
        });
    };

    render() {
        const {scrollIntoValue, selectedDates} = this.state;

        return (
            <div>
                <div style={{marginBottom: 16, padding: 12, background: '#f0f2f5', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>动态滚动控制</h4>
                    <Space>
                        <Button onClick={() => this.scrollToDate('2023-01-15')}>
                            滚动到 2023-01
                        </Button>
                        <Button onClick={() => this.scrollToDate('2023-06-15')}>
                            滚动到 2023-06
                        </Button>
                        <Button onClick={() => this.scrollToDate('2023-12-15')}>
                            滚动到 2023-12
                        </Button>
                        <Button onClick={() => this.scrollToDate('2024-03-15')}>
                            滚动到 2024-03
                        </Button>
                    </Space>
                </div>

                <div style={{marginBottom: 16, padding: 12, background: '#fff7e6', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>说明</h4>
                    <p>• <strong>当前滚动位置：</strong>{scrollIntoValue.format('YYYY-MM-DD')}</p>
                    <p>• <strong>显示时区：</strong>Asia/Shanghai</p>
                    <p>• <strong>存储时区：</strong>UTC</p>
                    <p>• <strong>模式：</strong>多选模式</p>
                    {selectedDates.length > 0 && (
                        <p style={{color: '#52c41a'}}>
                            • <strong>已选中 {selectedDates.length} 个日期：</strong>
                            {selectedDates.join(', ')}
                        </p>
                    )}
                </div>

                <Calendar
                    mutiple
                    scrollIntoValue={scrollIntoValue}
                    timezone="Asia/Shanghai"
                    serverTimezone="UTC"
                    enableTimezone={true}
                    onChange={this.onChange}
                    style={{margin: 10}}
                    fullscreen={false}
                />

                <div style={{marginTop: 16, padding: 12, background: '#e6f7ff', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>功能说明</h4>
                    <p><strong>scrollIntoValue 特性：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>支持 Moment 类型的动态滚动</li>
                        <li>自动进行时区转换（Moment 视为 timezone）</li>
                        <li>多选模式下滚动到指定月份</li>
                        <li>点击日期可选中/取消选中</li>
                    </ul>
                    <p style={{margin: 0}}>
                        💡 <strong>提示：</strong>点击按钮可以快速滚动到不同月份
                    </p>
                </div>
            </div>
        );
    }
}

export default Demo40;
```
