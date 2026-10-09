---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 时区 - 性能优化与禁用

演示同时区自动禁用转换和 enableTimezone 开关。

```tsx
import {Calendar, Button, Space, Switch} from '@tinper/next-ui';
import moment, {Moment} from 'moment';
import React, {Component} from 'react';

interface Demo39State {
    enableTimezone: boolean;
    scenario: 'same' | 'different';
    selectedValue: string | null;
}

class Demo39 extends Component<{}, Demo39State> {
    state: Demo39State = {
        enableTimezone: true,
        scenario: 'same',
        selectedValue: null
    };

    onChange = (value: Moment) => {
        const formatted = value.format('YYYY-MM-DD HH:mm:ss');
        console.log('onChange:', formatted);
        this.setState({selectedValue: formatted});
    };

    toggleTimezone = (checked: boolean) => {
        this.setState({enableTimezone: checked, selectedValue: null});
    };

    setScenario = (scenario: 'same' | 'different') => {
        this.setState({scenario, selectedValue: null});
    };

    render() {
        const {enableTimezone, scenario, selectedValue} = this.state;
        const isSameTimezone = scenario === 'same';

        return (
            <div>
                <div style={{marginBottom: 16, padding: 12, background: '#f0f2f5', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>配置控制</h4>
                    <Space>
                        <div>
                            <label style={{marginRight: 8}}>时区转换开关：</label>
                            <Switch checked={enableTimezone} onChange={this.toggleTimezone} />
                            <span style={{marginLeft: 8}}>
                                {enableTimezone ? '已启用' : '已禁用'}
                            </span>
                        </div>
                    </Space>
                    <div style={{marginTop: 12}}>
                        <label style={{marginRight: 8}}>测试场景：</label>
                        <Space>
                            <Button
                                type={isSameTimezone ? 'primary' : 'default'}
                                onClick={() => this.setScenario('same')}
                            >
                                同时区（性能优化）
                            </Button>
                            <Button
                                type={!isSameTimezone ? 'primary' : 'default'}
                                onClick={() => this.setScenario('different')}
                            >
                                不同时区
                            </Button>
                        </Space>
                    </div>
                </div>

                <div style={{marginBottom: 16, padding: 12, background: '#fff7e6', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>当前配置</h4>
                    <p>• <strong>enableTimezone：</strong>{enableTimezone ? '✅ true（启用转换）' : '❌ false（禁用转换）'}</p>
                    <p>• <strong>timezone：</strong>Asia/Shanghai 2023-06-15 14:00:00</p>
                    <p>• <strong>serverTimezone：</strong>{isSameTimezone ? 'Asia/Shanghai' : 'America/New_York'}</p>
                    <p>• <strong>性能优化：</strong>
                        {isSameTimezone ? '✅ 自动禁用转换（timezone === serverTimezone）' : '❌ 需要转换'}
                    </p>
                    {selectedValue && (
                        <p style={{color: '#52c41a'}}>
                            • <strong>选中回调值：</strong>{selectedValue}
                        </p>
                    )}
                </div>

                <Calendar
                    value={moment('2023-06-15 14:00:00')}
                    timezone="Asia/Shanghai"
                    serverTimezone={isSameTimezone ? 'Asia/Shanghai' : 'America/New_York'}
                    enableTimezone={enableTimezone}
                    onChange={this.onChange}
                    style={{margin: 10}}
                    fullscreen={false}
                />

                <div style={{marginTop: 16, padding: 12, background: '#e6f7ff', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>测试说明</h4>
                    <p><strong>场景1 - 同时区（性能优化）：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>timezone 和 serverTimezone 都是 Asia/Shanghai</li>
                        <li>系统自动禁用时区转换，提升性能</li>
                        <li>即使 enableTimezone=true，也不会进行转换</li>
                    </ul>
                    <p><strong>场景2 - 不同时区：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>timezone: Asia/Shanghai，serverTimezone: America/New_York</li>
                        <li>enableTimezone=true 时进行时区转换</li>
                        <li>enableTimezone=false 时禁用转换</li>
                    </ul>
                </div>
            </div>
        );
    }
}

export default Demo39;
```
