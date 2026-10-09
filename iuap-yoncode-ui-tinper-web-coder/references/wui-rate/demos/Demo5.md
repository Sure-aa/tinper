---
tags:
  - TinperNext
  - rate组件
---
# 评分 Rate

## 只读

只读，无法进行鼠标交互。

```tsx
import {Rate} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo5 extends Component {
    render() {
        return (
            <Rate defaultValue={4} disabled/>
        )
    }
}

export default Demo5;
```
