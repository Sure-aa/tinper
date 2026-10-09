---
tags:
  - TinperNext
  - timeline组件
---
# 时间轴 Timeline

## fieldid

给节点添加fieldid属性

```tsx
import React, { Component } from 'react';
import { Timeline } from '@tinper/next-ui';

class Demo5 extends Component {
    render() {
        return (
            <Timeline fieldid={'field'} id={'timeline'}>
                <Timeline.Item id={'first'}>Create a services site 2015-09-01</Timeline.Item>
                <Timeline.Item>Solve initial network problems 2015-09-01</Timeline.Item>
                <Timeline.Item fieldid={'three'}>Technical testing 2015-09-01</Timeline.Item>
                <Timeline.Item>Network problems being solved 2015-09-01</Timeline.Item>
            </Timeline>
        )
    }
}


export default Demo5;
```
