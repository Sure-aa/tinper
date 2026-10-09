---
tags:
  - TinperNext
  - spin组件
---
# 加载提示 Spin

## 容器

指定`getPopupContainer`属性为`this`，可显示在该组件的上面。

```tsx
import {Spin} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <div className="demo2" id="demo2">
                <Spin getPopupContainer={() => document.querySelector('#demo2')} spinning={true}>
                </Spin>
            </div>
        )
    }
}

export default Demo2;
```
