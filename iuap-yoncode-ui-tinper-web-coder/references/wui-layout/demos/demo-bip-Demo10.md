---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## flex填充

使用<Row>组件和<Col>组件进行页面栅格切分
* Demo10

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo10 extends Component {
    render() {
        return (
            <div>
                <Row>
                    <Col className='grayDeep' flex={2}>2 / 5</Col>
                    <Col className='gray' flex={3}>3 / 5</Col>
                </Row>
                <Row>
                    <Col className='grayDeep' flex="100px">100px</Col>
                    <Col className='gray' flex="auto">Fill Rest</Col>
                </Row>
            </div>
        )
    }
}

export default Demo10;
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
