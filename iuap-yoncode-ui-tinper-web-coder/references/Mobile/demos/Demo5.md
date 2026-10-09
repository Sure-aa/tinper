---
tags:
  - TinperNextPro
  - Mobile组件
---
# Mobile 手机号

## 只读禁用状态
手机号组件只读禁用状态显示

```tsx
import React from "react";
import Mobile from "tne-tinpernextpro-fe/Mobile";
import "./demo.less";

const LayoutDemo = () => {
  return (
    <>
      <Mobile readOnly value="12345678901" />
      <br/>
      <Mobile disabled value="12345678901" />
    </>
  );
};
export default LayoutDemo;
```

```less

```
