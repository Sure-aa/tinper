---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 平移的栅格

通过设置mdPull, mdPush来控制平移的量

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo3 extends Component {
    render() {
        return (
            <Row>
                <Col md={8} mdPush={4} xs={8} xsPush={4} sm={8} smPush={4}>
                    <div className='grayDeep'>8 push-4</div>
                </Col>
                <Col span={4} pull={8}>
                    <div className='gray'>4 pull-8</div>
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
