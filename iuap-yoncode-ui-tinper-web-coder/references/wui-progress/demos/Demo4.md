---
tags:
  - TinperNext
  - progress组件
---
# 进度条 Progress

## 小型进度圈

小一号的圈形进度。

```tsx
import {Progress} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo4 extends Component {
    render() {
        return (
            <div>
                <Progress type="circle" percent={30} width={80} />
                <Progress type="circle" percent={70} width={80} status="exception"/>
                <Progress type="circle" percent={100} width={80}/>
            </div>
        )
    }
}

export default Demo4
```
