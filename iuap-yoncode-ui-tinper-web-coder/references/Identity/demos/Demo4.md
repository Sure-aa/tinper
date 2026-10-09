---
tags:
  - TinperNextPro
  - Identity组件
---
# Identity 证件号

## 只读禁用状态
证件号组件只读禁用状态显示

```tsx
import React from "react";
import { Identity } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {

  return (
    <>
      <Identity readOnly value={{ identity: '412702', idType: '1' }}></Identity>
      <br/>
      <Identity disabled value={{ identity: '412702', idType: '1' }}></Identity>
    </>
  );
};
export default LayoutDemo;
```
