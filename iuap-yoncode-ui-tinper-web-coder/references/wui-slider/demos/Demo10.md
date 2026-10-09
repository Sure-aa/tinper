---
tags:
  - TinperNext
  - slider组件
---
# 滑块 Slider

## 允许清除

设置 allowClear 单滑块模式有效

```tsx
import {Slider} from "@tinper/next-ui";
import React, {Component} from 'react';

const style = {width: 400, margin: 50, marginBottom: 60};

class Demo10 extends Component {
    render() {
        return (
            <div>
                <div style={style}>
                    <Slider allowClear defaultValue={20}/>
                </div>
            </div>
        )
    }
}


export default Demo10;
```
