---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

## 校验示例
电话号组件校验示例（查看控制台提示）

```tsx
import React from "react";
import { Phone } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  return (
    <>
      <Phone noExtension={false} value={{H: "1234567", E: "1234"}} required onSuccess={(value: any) => console.log("onSuccess====>", value)} onError={(value: any, cityCode: string) => console.log("onError====>", value, cityCode)}/>
    </>
  );
};
export default LayoutDemo;
```
