---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 时区 - 小时视图 + 时间事件

演示小时视图下的 timeEvents 时区转换和 onCreateEvent 回调。

```tsx
import {Calendar} from '@tinper/next-ui';
import moment, {Moment} from 'moment';
import React, {Component} from 'react';

interface Demo37State {
    createdEvents: any[];
}

const today = moment().format('YYYY-MM-DD');

class Demo37 extends Component<{}, Demo37State> {
    state: Demo37State = {
        createdEvents: [],
    };

    // timeEvents 使用 serverTimezone (America/New_York)
    timeEvents: any[] = [
        {
            start: today + ' 09:00:00', // 纽约时间 9:00
            end: today + ' 10:00:00', // 纽约时间 10:00
            content: '晨会（纽约时间 9:00）',
        },
        {
            start: today + ' 14:00:00', // 纽约时间 14:00
            end: today + ' 15:30:00', // 纽约时间 15:30
            content: '项目讨论（纽约时间 14:00）',
        }
    ]

    onTimeEventsClick = (e: React.MouseEvent<HTMLElement>, value: any, time: Moment) => {
        e.stopPropagation();
        console.log(e, value, time)
    }

     // 拖拽鼠标松开时的回调，此时参数为拖拽的起止时间，起止时间都是America/New_York时区的时间
     onCreateEvent = (val: {start: string, end: string}) => {
         console.log('onCreateEvent', val)
     }

     render() {
         const {createdEvents} = this.state;

         return (
             <div>
                 <div style={{marginBottom: 16, padding: 12, background: '#f0f2f5', borderRadius: 4}}>
                     <h4 style={{marginTop: 0}}>说明</h4>
                     <p>• <strong>视图类型：</strong>小时视图（Hour）</p>
                     <p>• <strong>显示时区：</strong>上海时区（Asia/Shanghai）</p>
                     <p>• <strong>存储时区：</strong>纽约时区（America/New_York）</p>
                     <p>• <strong>事件转换：</strong></p>
                     <ul style={{marginTop: 4, paddingLeft: 20}}>
                         <li>晨会: 纽约 09:00 → 上海 21:00 或 22:00（前一天）</li>
                         <li>项目讨论: 纽约 14:00 → 上海 02:00 或 03:00（次日）</li>
                     </ul>
                     {createdEvents.length > 0 && (
                         <div>
                             <p style={{color: '#52c41a', marginBottom: 4}}>
                                • <strong>已创建的事件：</strong>
                             </p>
                             {createdEvents.map((event, index) => (
                                 <p key={index} style={{margin: '4px 0', paddingLeft: 16}}>
                                     {index + 1}. {event.displayStart} ~ {event.displayEnd}
                                 </p>
                             ))}
                         </div>
                     )}
                 </div>

                 <Calendar
                     operations={['lastDay', 'lastMonth', 'nextDay', 'nextMonth', 'today', 'headerSwitcher']}
                     type="hour"
                     timezone="Asia/Shanghai"
                     serverTimezone="America/New_York"
                     enableTimezone={true}
                     fullscreen
	                mutiple
	                locale='zh-cn'
	                layout='left'
                     timeEvents={this.timeEvents}
                     onCreateEvent={this.onCreateEvent}
                     onTimeEventsClick={this.onTimeEventsClick}
                     showTimeLine
                     isDragEvent={true}
                 />

                 <div style={{marginTop: 16, padding: 12, background: '#e6f7ff', borderRadius: 4}}>
                     <p style={{margin: 0}}>
                        💡 <strong>提示：</strong>拖拽创建新事件，回调会返回 America/New_York 时区的时间
                     </p>
                 </div>
             </div>
         );
     }
}

export default Demo37;
```
