---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 自定义响应尺寸

使用size设置响应式规则，响应范围需要涵盖屏幕所有范围 例如：{sm:'(max-width: 1000px)',md:'(min-width: 1000px)'}

```tsx
import {Col, Row} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo extends Component {
    render() {
        return (
            <Row size={{
                'xs': '(max-width: 768px)',
                'sm': '(min-width: 768px)',
                'md': '(min-width: 992px)',
                'lg': '(min-width: 1200px)'
            }}>
                <Col span={12}>
                    <div className='grayDeep'>1</div>
                </Col>
                <Col lg={6} md={12} sm={12} xs={24} >
                    <div className='grayLight'>2</div>
                </Col>
                <Col sm={6} xs={12}>
                    <div className='grayDeep'>3</div>
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
