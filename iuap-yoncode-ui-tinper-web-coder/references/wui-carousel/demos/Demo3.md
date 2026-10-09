---
tags:
  - TinperNext
  - carousel组件
---
# 走马灯 Carousel

## 自动切换

定时切换下一张。

```tsx
import {Carousel} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo3 extends Component {
    render() {
        return (
            <Carousel autoplay>
                <div>
                    <h3>1</h3>
                </div>
                <div>
                    <h3>2</h3>
                </div>
                <div>
                    <h3>3</h3>
                </div>
                <div>
                    <h3>4</h3>
                </div>
            </Carousel>
        )
    }
}

export default Demo3
```
