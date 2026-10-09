---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 时区 - 基础日期选择（Moment 类型）

演示 Moment 类型的 value 被视为 timezone，屏蔽 deviceUTC 影响。

```tsx
import {Calendar} from '@tinper/next-ui';
import {Moment} from 'moment';
import React, {Component} from 'react';

interface Demo35State {
    selectedValue: string | null;
}

class Demo35 extends Component<{}, Demo35State> {
    state: Demo35State = {
        selectedValue: null
    };

    onChange = (value: Moment) => {
        console.log('onChange - 转换为 serverTimezone (UTC):', value.format('YYYY-MM-DD HH:mm:ss'));
        this.setState({
            selectedValue: value.format('YYYY-MM-DD HH:mm:ss')
        });
    };

    onSelect = (value: Moment) => {
        console.log('onSelect - 转换为 serverTimezone (UTC):', value.format('YYYY-MM-DD HH:mm:ss'));
    };

    render() {
        const {selectedValue} = this.state;

        return (
            <div>
                <div style={{marginBottom: 16, padding: 12, background: '#f0f2f5', borderRadius: 4}}>
                    {selectedValue && (
                        <p style={{color: '#52c41a'}}>
                            • <strong>选中回调值：</strong>{selectedValue} (UTC)
                        </p>
                    )}
                </div>

                <Calendar
                    timezone="Asia/Shanghai"
                    serverTimezone="UTC"
                    enableTimezone={true}
                    onChange={this.onChange}
                    onSelect={this.onSelect}
                    style={{margin: 10}}
                    fullscreen={false}
                />

                <div style={{marginTop: 16, padding: 12, background: '#e6f7ff', borderRadius: 4}}>
                    <p style={{margin: 0}}>
                        💡 <strong>提示：</strong>Moment 类型不受设备本地时区影响，始终按 timezone 解析
                    </p>
                </div>
            </div>
        );
    }
}

export default Demo35;
```
