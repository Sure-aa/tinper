---
tags:
  - TinperNext
  - button组件
---
# 按钮 Button

## 基础按钮

基础的按钮用法。

```tsx
import {Button} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo1 extends Component {
    open() {
        alert("onClick");
    }

    render() {
        return (
            <div className="demoPadding">
                <Button>默认按钮</Button>
                <Button colors="primary" onClick={this.open}>主要按钮</Button>
                <Button colors="secondary">次按钮</Button>
                <Button colors="dark">页面次按钮</Button>
                <Button type="plainText">文本按钮</Button>
            </div>
        )
    }
}

export default Demo1;
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
