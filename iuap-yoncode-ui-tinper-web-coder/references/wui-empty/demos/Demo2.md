---
tags:
  - TinperNext
  - empty组件
---
# 空状态 Empty

## 自定义占位图

image传入替换图片地址。

```tsx
import {Empty} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <Empty image="https://img1.baidu.com/it/u=3009731526,373851691&fm=253&app=138&size=w931&n=0&f=JPEG&fmt=auto?sec=1668790800&t=853197e94e933ec5472f70410744b01c"/>
        )
    }
}

export default Demo2;
```
