---
tags:
  - TinperNext
  - card组件
---
# 卡片 Card

## 无边框类型

在灰色背景上使用无边框的卡片

```tsx
import {Card} from "@tinper/next-ui";
import React, {Component} from 'react';


class Demo2 extends Component {
    render() {
        return (
            <div className="no-border-card-box">
                <Card title="Card title" bordered={false} style={{width: 300}}>
                    <p>Card content</p>
                    <p>Card content</p>
                    <p>Card content</p>
                </Card>
            </div>
        )
    }
}


export default Demo2;
```

```css
.no-border-card-box {
  padding: 30px;
  background: #eee;
}
```
