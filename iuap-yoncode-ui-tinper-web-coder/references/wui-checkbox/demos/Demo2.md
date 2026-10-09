---
tags:
  - TinperNext
  - checkbox组件
---
# 多选 Checkbox

## 不同颜色的 Checkbox

`colors`参数控制背景色

```tsx
import {Checkbox} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo2 extends Component {
    render() {
        return (
            <div className="demo-checkbox">
                <span>默认模式：</span>
                <Checkbox colors="primary">primary</Checkbox>
                <Checkbox colors="success">success</Checkbox>
                <Checkbox colors="info">info</Checkbox>
                <Checkbox colors="danger">danger</Checkbox>
                <Checkbox colors="warning">warning</Checkbox>
                <Checkbox colors="dark">dark</Checkbox>
                <br />
                <br />
                <span>inverse 模式：</span>
                <Checkbox colors="primary" inverse>primary</Checkbox>
                <Checkbox colors="success" inverse>success</Checkbox>
                <Checkbox colors="info" inverse>info</Checkbox>
                <Checkbox colors="danger" inverse>danger</Checkbox>
                <Checkbox colors="warning" inverse>warning</Checkbox>
                <Checkbox colors="dark" inverse>dark</Checkbox>
            </div>
        )
    }
}

export default Demo2;
```
