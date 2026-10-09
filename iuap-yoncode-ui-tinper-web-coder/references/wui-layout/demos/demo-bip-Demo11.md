---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## order 排序

通过 order 来改变元素的排序。
* Demo10

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo extends Component {
    render() {
        return (
            <div>
                <Row>
                    <Col order={4} span={6}>
                        <div className='grayDeep'>col-1-order-4</div>
                    </Col>
                    <Col order={3} span={6}>
                        <div className='gray'>col-2-order-3</div>
                    </Col>
                    <Col order={2} span={6}>
                        <div className='grayLight'>col-3-order-2</div>
                    </Col>
                    <Col order={1} span={6}>
                        <div className='grayDeep'>col-4-order-1</div>
                    </Col>
                </Row>
            </div>
        )
    }
}

export default Demo;
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
