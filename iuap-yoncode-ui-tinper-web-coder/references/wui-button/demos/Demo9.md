---
tags:
  - TinperNext
  - button组件
---
# 按钮 Button

## 禁用状态

按钮不可用状态。

```tsx
import {Button} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo extends Component {
    render() {
        return (
            <div className="demoPadding">
                <Button disabled>默认按钮</Button>
                <Button disabled uirunmode="design" colors="primary">主要按钮</Button>
                <Button disabled colors="secondary">次按钮</Button>
                <Button disabled colors="dark">页面次按钮</Button>
                <Button disabled type="plainText">文本按钮</Button>
                <br/>
                <br/>
                <Button disabled bordered>默认按钮</Button>
                <Button disabled bordered colors="primary">主要按钮</Button>
            </div>
        )
    }
}

export default Demo;
```

```css
.demoPadding {
  button {
    margin: auto 5px;
  }

  .divider {
    margin: 6px 0;
    height: 1px;
    overflow: hidden;
    background-color: #fff;
  }
}

.el-icon--right {
  margin-left: 4px;
}
```
