---
tags:
  - TinperNext
  - progress组件
---
# 进度条 Progress

## 小型进度条

适合放在较狭窄的区域内。

```tsx
import {Progress} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo3 extends Component {
    render() {
        return (
            <div style={{width: 170}}>
                <Progress percent={30} size="small"/>
                <Progress percent={50} size="small" status="active"/>
                <Progress percent={70} size="small" status="exception"/>
                <Progress percent={100} size="small"/>
            </div>
        )
    }
}

export default Demo3
```
