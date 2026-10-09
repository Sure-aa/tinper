---
tags:
  - TinperNext
  - badge组件
---
# 标记 Badge

## 状态标识示例

使用status控制标识状态。

```tsx
import {Badge} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo1 extends Component {
    render() {
        return (
            <div>
                <Badge status="error" style={{marginRight: 20}} text="已停用"/>
                <Badge status="success" style={{marginRight: 20}} text="已启用"/>
                <Badge status="dark" style={{marginRight: 20}} text="未发布"/>
                <Badge status="warning" style={{marginRight: 20}} text="警示"/>
            </div>
        )
    }
}

export default Demo1;
```
