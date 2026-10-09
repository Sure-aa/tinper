---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

## 带分机号
电话号组件带分机号显示

```tsx
import React from "react";
import { Phone } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  return (
    <>
      <Phone noExtension={false} placeholder={{H: "123", E: "456"}}/>
    </>
  );
};
export default LayoutDemo;
```
