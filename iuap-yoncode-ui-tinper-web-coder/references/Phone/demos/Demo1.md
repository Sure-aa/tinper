---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

## 基础组件
电话号组件基础使用。

```tsx
import React from "react";
import { Phone } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  return (
    <>
      <Phone fieldid="phone-test" placeholder={{H: "123", E: ""}}/>
    </>
  );
};
export default LayoutDemo;
```
