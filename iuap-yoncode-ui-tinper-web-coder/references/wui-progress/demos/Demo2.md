---
tags:
  - TinperNext
  - progress组件
---
# 进度条 Progress

## 进度圈

圈形的进度。

```tsx
import {Progress} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <div>
                <Progress type="circle" percent={75}/>
                <Progress type="circle" percent={70} status="exception"/>
                <Progress type="circle" percent={100}/>
                {/* <Progress type="circle" percent={100} strokeWidth={40} width={400}	 /> */}
            </div>
        )
    }
}

export default Demo2
```
