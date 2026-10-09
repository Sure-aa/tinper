---
tags:
  - TinperNext
  - tag组件
---
# 标签 Tag

## 默认标签

默认提供两种形式的标签，主要用于信息标注。

```tsx
import {Icon, Tag} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo1 extends Component {
    render() {
        return (
            <div className="demoPadding">
                <Tag>默认</Tag>
                <Tag color="light" bordered>边框标签</Tag>
                <Tag icon={<Icon type="uf-piechart"/>} bordered>自定义icon</Tag>
            </div>
        )
    }
}

export default Demo1;
```

```css
.demoPadding {
  .divider {
    margin: 6px 0;
    height: 1px;
    overflow: hidden;
    background-color: #fff;
  }
}
```
