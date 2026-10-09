---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

## 自定义多语请求逻辑
自定义远程请求配置

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

 function getRemoteResources(locale, tenantId) {
    return new Promise((resolve, reject) => {
      console.log(locale, tenantId, "当前语种；以及 租户");
      resolve({
        zhcn: {
          'UID:P_FW_1A5CED8805E8ddd': '测试getRemoteResources',
        },
        enus:{
          'UID:P_FW_1A5CED8805E8ddd': 'testgetRemoteResources',
        }
      });
    });
  }
  return (
    <>
      <ProConfigProvider 
        fieldid="phone-test" 
        pack={{
          "zhcn":{
            "P_YS_HR_HREM-FE_1591819943477248181": "批量业务最多支持<%=maxNum%>条数据"
          }
        }}
        getRemoteResources={getRemoteResources}
      >
               {
                (config)=>{
                  return <>
                      <Pagination showSizeChanger pageSizeOptions={["10", "20", "30", "50", "80"]} total={300} defaultPageSize={20} current={1} />
                      <p>多语言分组示例：{window.lang.templateByUuid("P_YS_HR_HREM-FE_1591819943477248181")}</p>
                      <p>自定义多语言请求的分组：{window.lang.templateByUuid("UID:P_FW_1A5CED8805E8ddd")}</p>
                     
                    </>
                }
               }

      </ProConfigProvider>
    </>
  );
};
export default LayoutDemo;
```
