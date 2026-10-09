---
tags:
  - TinperNext
  - space组件
---
# 间距 Space

## 自动换行

自动换行。

```tsx
import {Button, Space} from '@tinper/next-ui';
import React from 'react';


const Demo = () => (
    <Space size={[8, 16]} wrap>
        {new Array(40).fill(null).map((_, index) => (
            // eslint-disable-next-line react/no-array-index-key
            <Button key={index}>Button</Button>
        ))}
    </Space>
);

export default Demo
```
