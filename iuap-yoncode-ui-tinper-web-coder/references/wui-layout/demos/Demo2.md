---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 偏移的栅格

使用mdOffset lgOffset smOffset xsOffset来设置栅格偏移的量

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <Row>
                <Col span={3} offset={3}>
                    <div className='grayDeep'>3 offset-3</div>
                </Col>
                <Col span={3} offset={3}>
                    <div className='gray'>3 offset-3</div>
                </Col>
                <Col span={6} offset={6}>
                    <div className='grayLight'>6 offset-6</div>
                </Col>
                <Col span={4} offset={2}>
                    <div className='gray'>4 offset-2</div>
                </Col>
                <Col span={4} offset={2}>
                    <div className='grayLight'>4 offset-2</div>
                </Col>
                <Col span={6} offset={2}>
                    <div className='grayDeep'>6 offset-2</div>
                </Col>
            </Row>
        )
    }
}

export default Demo2;
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
