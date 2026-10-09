---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

## 在线多语配置
基础使用方法,配置groupCode直接走在线多语

```tsx
import React from "react";
import { ProConfigProvider } from "tne-tinpernextpro-fe";
import {Pagination, Form, Input, Icon} from '@tinper/next-ui';


const LayoutDemo = () => {
  const formItemLayout = {
  labelCol: {
      xs: { span: 4 },
      sm: { span: 4 }
  },
  wrapperCol: {
      xs: { span: 8 },
      sm: { span: 8 }
  }
};
  return (
    <>
      <ProConfigProvider fieldid="phone-test" groupCode="YS_FED_CORE-YNF-FE">
               {
                (config)=>{
                  
                  return <>
                      <Pagination showSizeChanger pageSizeOptions={["10", "20", "30", "50", "80"]} total={300} defaultPageSize={20} current={1} />
                      <p>多语言分组示例：{window.lang.templateByUuid("UID:P_CORE-YNF-FE_1F463A9005F8003F")}</p>
                    </>
                }
               }

      </ProConfigProvider>
    </>
  );
};
export default LayoutDemo;
```
