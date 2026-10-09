---
tags:
  - TinperNext
  - locale组件
---
# 多语 Locale

## 多语组件设置组件的语言

按照固定的格式传入语言对象，会自动改变组件内默认文字的语言。

```tsx
import {Button, Locale, Popconfirm, EnUS as En} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo1 extends Component {
    render() {
        let content = 'Do yon like me?';
        return (
            <Locale locale={En}>
                <Popconfirm
                    trigger="click"
                    placement="right"
                    content={content}>
                    <Button colors="primary">see right!</Button>
                </Popconfirm>
            </Locale>
        )
    }
}

export default Demo1;
```
