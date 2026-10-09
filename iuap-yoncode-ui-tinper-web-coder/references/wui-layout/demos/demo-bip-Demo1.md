---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 基础布局

使用<Row>组件和<Col>组件进行页面栅格切分

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo1 extends Component {
    render() {
        return (
            <Row>
                <Col span={12}>
                    <div className='grayDeep'>12</div>
                </Col>
                <Col span={6}>
                    <div className='gray'>6</div>
                </Col>
                <Col span={6}>
                    <div className='grayLight'>6</div>
                </Col>
                <Col span={4}>
                    <div className='grayDeep'>4</div>
                </Col>
                <Col span={4}>
                    <div className='gray'>4</div>
                </Col>
                <Col span={4}>
                    <div className='grayLight'>4</div>
                </Col>
                <Col span={3}>
                    <div className='grayDeep'>3</div>
                </Col>
                <Col span={3}>
                    <div className='gray'>3</div>
                </Col>
                <Col span={3}>
                    <div className='grayLight'>3</div>
                </Col>
                <Col span={3}>
                    <div className='grayDeep'>3</div>
                </Col>
                <Col span={2}>
                    <div className='gray'>2</div>
                </Col>
                <Col sm={2}>
                    <div className='grayLight'>2</div>
                </Col>
                <Col xl={2} md={4} sm={6} xs={12}>
                    <div className='gray'>2</div>
                </Col>
                <Col lg={2} md={4} sm={6} xs={12} >
                    <div className='grayLight'>2</div>
                </Col>
                <Col md={4} sm={6} xs={12}>
                    <div className='grayDeep'>2</div>
                </Col>
            </Row>
        )
    }
}

export default Demo1;
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
