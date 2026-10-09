---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

## 只读禁用状态
只读禁用状态显示

```tsx
import React from "react";
import { Phone } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
    return (
        <>
            <Phone readOnly value={{ H: "123", E: "456" }} />
            <br/>
            <Phone disabled value={{ H: "123", E: "456" }} />
        </>
    );
};
export default LayoutDemo;
```
