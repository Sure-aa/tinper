---
tags:
  - TinperNext
  - tag组件
---
# 标签 Tag

## disable标签

禁用的标签，不可以进行编辑。

```tsx
import {Tag} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo3 extends Component {
    render() {
        return (
            <div className="demoPadding">
                <Tag disabled>disabled</Tag>
            </div>
        )
    }
}

export default Demo3;
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
