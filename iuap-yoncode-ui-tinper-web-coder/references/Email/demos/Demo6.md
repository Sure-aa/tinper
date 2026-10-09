---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 只读禁用状态
邮箱组件只读禁用状态显示

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {

  return (
    <>
      <Email readOnly value="hello123" ></Email>
      <br/>
      <Email disabled value="hello123" ></Email>
    </>
  );
};
export default LayoutDemo;
```
