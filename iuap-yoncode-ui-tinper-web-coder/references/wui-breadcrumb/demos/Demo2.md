---
tags:
  - TinperNext
  - breadcrumb组件
---
# 面包屑 Breadcrumb

## 图标

使用Icon图标组件。

```tsx
import {Breadcrumb, Icon} from '@tinper/next-ui';
import React, {Component} from 'react';


class Demo2 extends Component {
    render() {
        return (
            <Breadcrumb>
                <Breadcrumb.Item target="_blank" href="https://yondesign.yonyoucloud.com/website/#/tinpernext">
                    <Icon type="uf-home"/>
                </Breadcrumb.Item>
                <Breadcrumb.Item>
                    <Icon type="uf-building-o"/>
                </Breadcrumb.Item>
                <Breadcrumb.Item active>
                    <Icon type="uf-files-o"/>
                </Breadcrumb.Item>
            </Breadcrumb>
        )
    }
}

export default Demo2;
```
