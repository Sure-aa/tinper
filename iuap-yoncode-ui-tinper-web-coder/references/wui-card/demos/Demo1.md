---
tags:
  - TinperNext
  - card组件
---
# 卡片 Card

## 基本使用

包含标题、内容、操作区域

```tsx
import {Card} from "@tinper/next-ui";
import React, {Component} from 'react';


class Demo1 extends Component {
    render() {
        return (
            <div>
                <Card fieldid="card" title="Default size card" extra={<a>More</a>} style={{width: 300}}>
                    <p>Card content</p>
                    <p>Card content</p>
                    <p>Card content</p>
                </Card>
                <br/>
                <Card size="small" title="Small size card" extra={<a>More</a>} style={{width: 300}}>
                    <p>Card content</p>
                    <p>Card content</p>
                    <p>Card content</p>
                </Card>
                <br/>
                <Card style={{width: 300}}>
                    <p>Card content</p>
                    <p>Card content</p>
                    <p>Card content</p>
                </Card>
            </div>
        )
    }
}


export default Demo1;
```

```css
.no-border-card-box {
  padding: 30px;
  background: #eee;
}
```
