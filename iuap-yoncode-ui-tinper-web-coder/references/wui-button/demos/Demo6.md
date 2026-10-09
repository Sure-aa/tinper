---
tags:
  - TinperNext
  - button组件
---
# 按钮 Button

## 加载中

加载中状态。

```tsx
import {Button} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo1 extends Component {

    render() {
        return (
            <div className="demoPadding">
                <Button loading colors="primary">加载中</Button>
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
