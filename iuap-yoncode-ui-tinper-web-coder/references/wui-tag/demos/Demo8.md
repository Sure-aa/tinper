---
tags:
  - TinperNext
  - tag组件
---
# 标签 Tag

## 自定义颜色

可以通过color属性控制标签的颜色

```tsx
import {Tag} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo6 extends Component {

    render() {
        return (
            <div className="demoPadding">
                <Tag color="rgba(39,211,129,0.75)">green</Tag>
                <Tag color="#2db7f5">#2db7f5</Tag>
            </div>
        )
    }
}

export default Demo6;
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
