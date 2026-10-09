---
tags:
  - TinperNext
  - divider组件
---
# 分割线 Divider

## 垂直分割线

设置type="vertical"，垂直分割，实线虚线两种类型，可在中间加入文字

```tsx
import {Divider} from '@tinper/next-ui';
import React, {Component} from "react";

class Demo2 extends Component {

    render() {
        return (
            <>
				Text
                <Divider type="vertical"/>
                <a href="https://yondesign.yonyoucloud.com/">Link</a>
                <Divider type="vertical"/>
                <a href="https://yondesign.yonyoucloud.com/">Link</a>
            </>
        );
    }
}

export default Demo2;
```

```css
.divider-class {
  background: none;
  border-color: #E9EBEC;
  border-style: dashed;
  border-width: 1px 0 0;
}
```
