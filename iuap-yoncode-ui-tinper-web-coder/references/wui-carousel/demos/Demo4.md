---
tags:
  - TinperNext
  - carousel组件
---
# 走马灯 Carousel

## 渐显

切换效果为渐显。

```tsx
import {Carousel} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo4 extends Component {
    render() {
        return (
            <Carousel effect="fade">
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

export default Demo4
```
