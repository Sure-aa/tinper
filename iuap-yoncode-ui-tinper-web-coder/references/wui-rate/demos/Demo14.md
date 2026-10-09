---
tags:
  - TinperNext
  - rate组件
---
# 评分 Rate

## 浏览态

browser开启浏览态

```tsx
import {Rate} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo14 extends Component {
    render() {
        return (
            <Rate defaultValue={4} browser/>
        )
    }
}

export default Demo14;
```
