---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

## 自适应layout布局
根据当前语种设置layout布局

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
      <ProConfigProvider 
        fieldid="phone-test" 
        locale="en_US"
        pack={{
          "enus":{
            "P_YS_HR_HREM-FE_1591819943477248181": "test"
          }
        }}

      >
               {
                (config)=>{
                  return <>
                      
                      <p>英文场景：</p>
                      <Form >
                          <Form.Item {...formItemLayout} label='混元一气上方太乙金仙美猴王齐天大圣斗战胜佛孙悟空' name='name' colon tooltip={'混元一气上方太乙金仙美猴王齐天大圣斗战胜佛孙悟空'}>
                              <Input placeholder='我的label会换行哦'/>
                          </Form.Item>
                            <Form.Item {...formItemLayout} label='混元一气上方太乙金仙美猴王齐天大圣斗战胜佛孙悟空' name='name' colon tooltip={{ title: '混元一气上方太乙金仙美猴王齐天大圣斗战胜佛孙悟空', icon: <Icon type="uf-filter"/> }}>
                          <Input placeholder='这是个直肠子label'/>
                        </Form.Item>
                        <Form.Item {...formItemLayout} label='住址' name='address' colon tooltip={{ title: '自定义图标', icon: <Icon title='' type="uf-earth"/> }}>
                            <Input placeholder='请输入地址'/>
                        </Form.Item>
                      </Form>
                    </>
                }
               }

      </ProConfigProvider>
    </>
  );
};
export default LayoutDemo;
```
