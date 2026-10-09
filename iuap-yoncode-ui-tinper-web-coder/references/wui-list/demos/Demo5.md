---
tags:
  - TinperNext
  - list组件
---
# 列表 List

## 自定义空数据展示

可使用emptyText自定义空数据展示内容

```tsx
import { Empty, List } from '@tinper/next-ui';
import React, { Component } from 'react';


class Demo extends Component {

    render() {
        return (
            <>
                <List />
                <List emptyText={<Empty description={"自定义空数据展示内容"} />} />
            </>
        )
    }
}

export default Demo;
```
