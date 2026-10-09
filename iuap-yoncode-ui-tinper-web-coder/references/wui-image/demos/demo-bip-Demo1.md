---
tags:
  - TinperNext
  - image组件
---
# 图片查看器 Image

## 单个图片查看

单个图片查看

```tsx
import { Image } from '@tinper/next-ui'
import React, { Component } from 'react';

class Demo1 extends Component<{}, {}> {

    render() {
        const src = "http://design.yonyoucloud.com/static/bee.tinper.org-demo/swiper-demo-1-min.jpg";
        return (
            <div className='demo'>
                <Image>
                    <img data-original={src} src={src} alt="Picture" />
                </Image>
            </div>
        )
    }
}

export default Demo1
```
