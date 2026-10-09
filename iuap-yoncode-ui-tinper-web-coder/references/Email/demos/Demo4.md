---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 规则校验
必填校验示例（查看控制台报错信息）

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [val3, setVal3] = React.useState("hello123");

  return (
    <>
        <Email
          check
          required
          value={val3}
          onChange={(val: any) => setVal3(val)}
          onSuccess={(val: any) => console.log("onSuccess====>", val)}
          onError={(_val: any, pattern: any) => {
            console.log("onError====>", _val, pattern);
          }}
        />
    </>
  );
};
export default LayoutDemo;
```
