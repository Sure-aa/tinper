---
tags:
  - TinperNext
  - clipboard组件
---
# 剪贴板 Clipboard

## 默认复制

在复制按钮中定义内容，点击复制到剪切板

```tsx
import {Clipboard} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo1 extends Component {
    render() {
        function success() {
            console.log('success');
        }

        function error() {
            console.log('error');
        }

        return (
            <Clipboard action="copy" text="默认复制-我将被复制到剪切板" success={success} error={error}>

            </Clipboard>
        )
    }
}

export default Demo1;
```
