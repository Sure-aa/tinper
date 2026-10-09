---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## gutter设置

设置row col 直接的的间距 第一个值为水平方向，第二个值为竖直方向
* Demo9

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo9 extends Component {
    render() {
        return (
            <div>
                <Row gutter={24}>
                    <Col span={12}>
                        <div className='grayDeep'>row-1-col-1</div>
                    </Col>
                    <Col span={12}>
                        <div className='gray'>row-1-col-2</div>
                    </Col>
                    <Col span={12}>
                        <div className='grayLight'>row-1-col-3</div>
                    </Col>
                    <Col span={12}>
                        <div className='grayDeep'>row-1-col-4</div>
                    </Col>
                </Row>
                <Row style={{overflow: 'hidden'}} gutter={{md: 24, sm: 12}}>
                    <Col span={12}>
                        <div className='grayDeep'>row-2-col-1</div>
                    </Col>
                    <Col span={12}>
                        <div className='gray'>row-2-col-2</div>
                    </Col>
                    <Col span={12}>
                        <div className='grayLight'>row-2-col-3</div>
                    </Col>
                    <Col span={12}>
                        <div className='grayDeep'>row-2-col-4</div>
                    </Col>
                </Row>
                <Row gutter={[24, 24]}>
                    <Col span={6}>
                        <div className='grayDeep'>row-3-col-1</div>
                    </Col>
                    <Col span={6}>
                        <div className='gray'>row-3-col-2</div>
                    </Col>
                    <Col span={6}>
                        <div className='grayLight'>row-3-col-3</div>
                    </Col>
                    <Col span={6}>
                        <div className='grayDeep'>row-3-col-4</div>
                    </Col>
                    <Col span={6}>
                        <div className='grayDeep'>row-3-col-5</div>
                    </Col>
                    <Col span={6}>
                        <div className='gray'>row-3-col-6</div>
                    </Col>
                    <Col span={6}>
                        <div className='grayLight'>row-3-col-7</div>
                    </Col>
                    <Col span={6}>
                        <div className='grayDeep'>row-3-col-8</div>
                    </Col>
                </Row>
            </div>
        )
    }
}

export default Demo9;
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
