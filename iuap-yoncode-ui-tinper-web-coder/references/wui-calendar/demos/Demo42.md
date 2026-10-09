---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 时区 - 综合集成测试

演示多选 + 时间事件 + 拖拽创建的完整时区功能集成。

```tsx
import {Calendar, Tabs, Badge} from '@tinper/next-ui';
import moment, {Moment} from 'moment';
import React, {Component} from 'react';

const {TabPane} = Tabs;

interface Demo42State {
    selectedDates: string[];
    createdEvents: any[];
    activeTab: string;
}

class Demo42 extends Component<{}, Demo42State> {
    state: Demo42State = {
        selectedDates: [],
        createdEvents: [],
        activeTab: '1'
    };

    // 时间事件（存储为 UTC）
    timeEvents = [
        {
            start: '2023-06-15 01:00:00', // UTC 01:00
            end: '2023-06-15 02:00:00', // UTC 02:00
            content: '团队站会',
            key: 'event1',
            color: '#1890ff'
        },
        {
            start: '2023-06-15 05:00:00', // UTC 05:00
            end: '2023-06-15 06:30:00', // UTC 06:30
            content: '产品评审',
            key: 'event2',
            color: '#52c41a'
        },
        {
            start: '2023-06-15 08:00:00', // UTC 08:00
            end: '2023-06-15 09:00:00', // UTC 09:00
            content: '技术分享',
            key: 'event3',
            color: '#faad14'
        }
    ];

    // 周时间事件（存储为 UTC）
    weekTimeEvents = {
        '2023-06-12': [
            {start: '2023-06-12 01:00:00', end: '2023-06-12 02:00:00', content: '周一早会', key: 'mon1', color: '#1890ff'}
        ],
        '2023-06-13': [
            {start: '2023-06-13 06:00:00', end: '2023-06-13 07:00:00', content: '周二培训', key: 'tue1', color: '#52c41a'}
        ],
        '2023-06-14': [
            {start: '2023-06-14 02:00:00', end: '2023-06-14 03:00:00', content: '周三站会', key: 'wed1', color: '#faad14'}
        ],
        '2023-06-15': [
            {start: '2023-06-15 05:00:00', end: '2023-06-15 06:00:00', content: '周四评审', key: 'thu1', color: '#eb2f96'}
        ],
        '2023-06-16': [
            {start: '2023-06-16 03:00:00', end: '2023-06-16 04:00:00', content: '周五总结', key: 'fri1', color: '#722ed1'}
        ]
    };

    onMultipleChange = (value: Moment, flag: boolean, valueStrings: string[]) => {
        console.log('多选模式 - onChange (UTC):', valueStrings);
        this.setState({selectedDates: valueStrings});
    };

    onCreateEvent = (eventData: any) => {
        console.log('创建事件 (UTC):', eventData);
        const {start, end, content = '新建事件'} = eventData;

        this.setState(prev => ({
            createdEvents: [
                ...prev.createdEvents,
                {
                    start,
                    end,
                    content,
                    createdAt: new Date().toLocaleString()
                }
            ]
        }));
    };

    render() {
        const {selectedDates, createdEvents, activeTab} = this.state;

        return (
            <div>
                <div style={{marginBottom: 16, padding: 12, background: '#f0f2f5', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>综合功能集成测试</h4>
                    <p>• <strong>显示时区：</strong>Asia/Shanghai（上海时区）</p>
                    <p>• <strong>存储时区：</strong>UTC</p>
                    <p>• <strong>集成功能：</strong>多选 + 时间事件 + 拖拽创建 + 时区转换</p>
                </div>

                <Tabs activeKey={activeTab} onChange={key => this.setState({activeTab: key})}>
                    <TabPane
                        tab={
                            <span>
                                多选模式
                                {selectedDates.length > 0 && (
                                    <Badge count={selectedDates.length} style={{marginLeft: 8}} />
                                )}
                            </span>
                        }
                        key="1"
                    >
                        <div style={{marginBottom: 16, padding: 12, background: '#fff7e6', borderRadius: 4}}>
                            <p style={{margin: 0}}>
                                <strong>已选中 {selectedDates.length} 个日期：</strong>
                                {selectedDates.length > 0 ? selectedDates.join(', ') : '（未选择）'}
                            </p>
                        </div>

                        <Calendar
                            mutiple
                            timezone="Asia/Shanghai"
                            serverTimezone="UTC"
                            enableTimezone={true}
                            onChange={this.onMultipleChange}
                            style={{margin: 10}}
                            fullscreen={false}
                        />
                    </TabPane>

                    <TabPane
                        tab={
                            <span>
                                小时视图 + 事件
                                {createdEvents.length > 0 && (
                                    <Badge count={createdEvents.length} style={{marginLeft: 8}} />
                                )}
                            </span>
                        }
                        key="2"
                    >
                        <div style={{marginBottom: 16, padding: 12, background: '#fff7e6', borderRadius: 4}}>
                            <p><strong>预设事件（UTC → 上海时区）：</strong></p>
                            <ul style={{marginTop: 4, paddingLeft: 20, marginBottom: 0}}>
                                <li>团队站会: UTC 01:00 → 上海 09:00</li>
                                <li>产品评审: UTC 05:00 → 上海 13:00</li>
                                <li>技术分享: UTC 08:00 → 上海 16:00</li>
                            </ul>
                        </div>

                        <Calendar
                            type="hour"
                            value={moment('2023-06-15')}
                            timezone="Asia/Shanghai"
                            serverTimezone="UTC"
                            enableTimezone={true}
                            timeEvents={this.timeEvents}
                            isDragEvent={true}
                            onCreateEvent={this.onCreateEvent}
                            showTimeLine={true}
                            style={{margin: 10}}
                        />

                        {createdEvents.length > 0 && (
                            <div style={{marginTop: 16, padding: 12, background: '#f6ffed', border: '1px solid #b7eb8f', borderRadius: 4}}>
                                <h4 style={{marginTop: 0}}>已创建的事件（UTC 时区）</h4>
                                {createdEvents.map((event, index) => (
                                    <div key={index} style={{marginBottom: 8, paddingBottom: 8, borderBottom: index < createdEvents.length - 1 ? '1px dashed #d9d9d9' : 'none'}}>
                                        <p style={{margin: '4px 0'}}>
                                            <strong>事件 {index + 1}：</strong>{event.content}
                                        </p>
                                        <p style={{margin: '4px 0', fontSize: 12, color: '#666'}}>
                                            时间: {event.start} ~ {event.end}
                                        </p>
                                        <p style={{margin: '4px 0', fontSize: 12, color: '#999'}}>
                                            创建于: {event.createdAt}
                                        </p>
                                    </div>
                                ))}
                            </div>
                        )}
                    </TabPane>

                    <TabPane tab="周视图 + 事件" key="3">
                        <div style={{marginBottom: 16, padding: 12, background: '#fff7e6', borderRadius: 4}}>
                            <p><strong>本周事件（UTC → 上海时区）：</strong></p>
                            <ul style={{marginTop: 4, paddingLeft: 20, marginBottom: 0}}>
                                <li>周一早会: UTC 01:00 → 上海 09:00</li>
                                <li>周二培训: UTC 06:00 → 上海 14:00</li>
                                <li>周三站会: UTC 02:00 → 上海 10:00</li>
                                <li>周四评审: UTC 05:00 → 上海 13:00</li>
                                <li>周五总结: UTC 03:00 → 上海 11:00</li>
                            </ul>
                        </div>

                        <Calendar
                            type="week"
                            value={moment('2023-06-15')}
                            timezone="Asia/Shanghai"
                            serverTimezone="UTC"
                            enableTimezone={true}
                            weekTimeEvents={this.weekTimeEvents}
                            isDragEvent={true}
                            onCreateEvent={this.onCreateEvent}
                            showTimeLine={true}
                            style={{margin: 10}}
                        />
                    </TabPane>
                </Tabs>

                <div style={{marginTop: 16, padding: 12, background: '#e6f7ff', borderRadius: 4}}>
                    <h4 style={{marginTop: 0}}>功能说明</h4>
                    <p><strong>多选模式：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>点击日期可选中/取消选中</li>
                        <li>onChange 回调返回所有选中日期的 UTC 时间</li>
                    </ul>
                    <p><strong>小时视图 + 事件：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>显示预设事件（从 UTC 转换为上海时区）</li>
                        <li>支持拖拽创建新事件</li>
                        <li>onCreateEvent 回调返回 UTC 时区的时间</li>
                    </ul>
                    <p><strong>周视图 + 事件：</strong></p>
                    <ul style={{paddingLeft: 20}}>
                        <li>显示整周的事件（从 UTC 转换为上海时区）</li>
                        <li>支持查看和创建全天事件</li>
                    </ul>
                    <p style={{margin: 0}}>
                        💡 <strong>核心特性：</strong>所有显示都是上海时区，所有回调都是 UTC 时区
                    </p>
                </div>
            </div>
        );
    }
}

export default Demo42;
```
