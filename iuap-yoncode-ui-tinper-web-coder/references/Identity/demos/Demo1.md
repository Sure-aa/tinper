---
tags:
  - TinperNextPro
  - Identity组件
---
# Identity 证件号

## 基础组件
证件号组件基础使用示例。

```tsx
import React from "react";
import { Identity } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [value, setValue] = React.useState({ identity: '412702', idType: '1' });

  const handleChange = (val) => {
    setValue(val)
  }
  return (
    <>
      <Identity value={value} onChange={handleChange} fieldid="identity-test"></Identity>
    </>
  );
};
export default LayoutDemo;
```
