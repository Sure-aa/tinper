---
tags:
  - TinperNextPro
  - Mobile组件
---
# Mobile 手机号

## 不带国际区号
手机号组件不带国际区号显示

```tsx
import React from "react";
import Mobile from "tne-tinpernextpro-fe/Mobile";
import "./demo.less";

const LayoutDemo = () => {
  return (
    <>
      <Mobile hideCountryCode />
    </>
  );
};
export default LayoutDemo;
```

```less

```
