---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 帮助文本
自定义帮助文本内容。

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [val2, setVal2] = React.useState("hello123");

  return (
    <>
      <Email value={val2} onChange={(val: any) => setVal2(val)} tips="这里是帮助文本"></Email>
    </>
  );
};
export default LayoutDemo;
```
