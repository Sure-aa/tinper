---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## wrap不换行

wrap默认为true，设置false,col不换行
* Demo11

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo extends Component {
    render() {
        return (
            <Row wrap={false}>
                <Col span={6}>
                    <div className='grayDeep'>col-1</div>
                </Col>
                <Col span={6}>
                    <div className='gray'>col-2</div>
                </Col>
                <Col span={6}>
                    <div className='grayLight'>col-3</div>
                </Col>
                <Col span={6}>
                    <div className='grayDeep'>col-4</div>
                </Col>
                <Col span={6}>
                    <div className='grayDeep'>col-5</div>
                </Col>
                <Col span={6}>
                    <div className='grayDeep'>col-6</div>
                </Col>
                <Col span={6}>
                    <div className='grayDeep'>col-7</div>
                </Col>
            </Row>
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
