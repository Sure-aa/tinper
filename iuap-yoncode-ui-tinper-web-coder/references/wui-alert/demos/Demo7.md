---
tags:
  - TinperNext
  - alert组件
---
# 平面提示 Alert

## 带边框的alert

带边框的alert

```tsx
import React from 'react';
import { Alert } from '@tinper/next-ui';

const Demo7: React.FC = () => (
    <Alert
        message="带边框的alert"
        type="success"
        bordered
        showIcon
        closable
    />
);

export default Demo7;
```
