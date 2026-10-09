---
tags:
  - TinperNext
  - card组件
---
# 卡片 Card

## 底部操作模块

放在普通卡片底部，支持操作按钮数组展示

```tsx
import {Card, Icon} from "@tinper/next-ui";
import React, {Component} from 'react';


class Demo6 extends Component {

    render() {
        return (
            <Card
                style={{width: 300}}
                actions={[
                    <Icon key="uf-pencil-s" type="uf-pencil-s"/>,
                    <Icon key="uf-del" type="uf-del"/>,
                    <Icon key="uf-repeat" type="uf-repeat"/>,
                ]}
            >
                <h3>Card content title</h3>
                <p>This is the description</p>
                <p>This is the description</p>
            </Card>
        )
    }
}


export default Demo6;
```

```css
.no-border-card-box {
  padding: 30px;
  background: #eee;
}
```
