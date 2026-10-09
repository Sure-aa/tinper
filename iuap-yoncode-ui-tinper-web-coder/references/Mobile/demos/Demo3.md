---
tags:
  - TinperNextPro
  - Mobile组件
---
# Mobile 手机号

## 帮助文本
手机号组件帮助文本。

```tsx
import React from "react";
import Mobile from "tne-tinpernextpro-fe/Mobile";
import { defaultCountryList } from './defaultCountryList'
import "./demo.less";

const LayoutDemo = () => {
  return (
    <>
      <Mobile countryList={defaultCountryList()} tips="这里是帮助文本" />
    </>
  );
};
export default LayoutDemo;
```

```less

```
