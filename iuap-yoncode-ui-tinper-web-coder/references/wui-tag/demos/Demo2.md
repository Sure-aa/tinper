---
tags:
  - TinperNext
  - tag组件
---
# 标签 Tag

## 默认标签

默认提供两种形式的标签，主要用于信息标注。

```tsx
import {Tag} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo extends Component {
    render() {
        return (
            <>
                <Tag>default</Tag>
                <Tag><span style={{ width: '100px', textOverflow: 'ellipsis', whiteSpace: 'nowrap', overflow: 'hidden'}}>较长的文本较长的文本较长的文本较长的文本较长的文本</span></Tag>
            </>
        )
    }
}

export default Demo;
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
