---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 栅格等分切换

通过设置grid, 实现栅格12、24等切换

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo3 extends Component {
    render() {
        return (
            <Row grid={12}>
                <Col span={3}>
                    <div className='grayDeep'>3</div>
                </Col>
                <Col span={3}>
                    <div className='gray'>3</div>
                </Col>
                <Col span={3}>
                    <div className='grayDeep'>3</div>
                </Col>
                <Col span={3}>
                    <div className='gray'>3</div>
                </Col>
            </Row>
        )
    }
}

export default Demo3;
```

```css
.grayDeep {
  background: #cdd9e6;
  height: 30px;
  margin-bottom: 10px;
  line-height: 30px;
  text-align: center;
}

.gray {
  background: #e1e8f0;
  height: 30px;
  margin-bottom: 10px;
  line-height: 30px;
  text-align: center;
}

.grayLight {
  background: #edf1f7;
  height: 30px;
  margin-bottom: 10px;
  color: rgb(66, 66, 66);
  text-align: center;
  line-height: 30px;
}
```
