---
tags:
  - TinperNext
  - avatar组件
---
# 头像 Avatar

## 响应式尺寸

头像大小可以根据屏幕大小自动调整

```tsx
import {Avatar, Icon} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo5 extends Component {
    render() {
        return (
            <Avatar
                size={{xs: 24, sm: 32, md: 40, lg: 64}}
                icon={<Icon type="uf-caven"/>}
            />
        )
    }
}

export default Demo5;
```

```css
.avatar-group {
  margin-top: 16px;
  display: flex;
  grid-column-gap: 16px;
  align-items: center;
}
```
