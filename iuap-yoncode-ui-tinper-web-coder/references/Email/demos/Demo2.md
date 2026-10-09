---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 自定义关联后缀
关联后缀自动填充。

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [val1, setVal1] = React.useState("hello123");
  const emailDomainList = ["example1.com", "example2.com", "example3.com", "example4.com"];

  return (
    <>
      <Email value={val1} onChange={(val: any) => setVal1(val)} emailDomainList={emailDomainList}></Email>
    </>
  );
};
export default LayoutDemo;
```
