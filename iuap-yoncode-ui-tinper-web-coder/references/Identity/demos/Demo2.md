---
tags:
  - TinperNextPro
  - Identity组件
---
# Identity 证件号

## 规则校验
自定义校验规则-必填校验（查看控制台错误提示信息）。

```tsx
import React from "react";
import { Identity } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [value1, setValue1] = React.useState({ identity: '412702', idType: '1' });

  const handleChange1 = (val: any) => {
    setValue1(val)
  }
  return (
    <>
      <Identity value={value1} onChange={handleChange1} showSelect={false} check required onError={(value: string, tag: string) => console.log("onError====>", value, tag)} onSuccess={(value: string) => console.log("onSuccess====>", value)} />
    </>
  );
};
export default LayoutDemo;
```
