---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 基础组件
邮箱组件基础使用方式。

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [val, setVal] = React.useState("hello123");

  return (
    <>
      <Email value={val} onChange={(val: any) => setVal(val)} fieldid="email-test" placeholder="请输入" ></Email>
    </>
  );
};
export default LayoutDemo;
```
