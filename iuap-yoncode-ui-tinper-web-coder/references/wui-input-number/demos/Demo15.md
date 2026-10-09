---
tags:
  - TinperNext
  - inputnumber组件
---
# 数字框 InputNumber

## minusRight 属性

负号在右边

```tsx
import {InputNumber} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo15 extends Component {
    render() {
        return (
            <div>
                <InputNumber
                    minusRight
                    value={-300}
                />
            </div>
        )
    }
}

export default Demo15;
```
