---
tags:
  - TinperNext
  - button组件
---
# 按钮 Button

## 文字按钮

没有边框和背景色的按钮。

```tsx
import {Button} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo extends Component {

    open() {
        alert("onClick");
    }

    render() {
        return (
            <div className="demoPadding">
                <Button type="text">文字按钮</Button>
                <Button ghost type="text">文字按钮反转颜色色</Button>
                <Button disabled bordered type="text">文字按钮</Button>
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
