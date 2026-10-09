---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

## 自定义本地词条
基础使用方法,配置pack直接走本地化多语以及自定义语种类型

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
      <ProConfigProvider fieldid="phone-test" locale="zh_CN" pack={{
        "zhcn":{
          "P_YS_HR_HREM-FE_1591819943477248181": "批量业务最多支持<%=maxNum%>条数据"
        }
      }}>
               {
                (config)=>{
                  return <>
                      <Pagination showSizeChanger pageSizeOptions={["10", "20", "30", "50", "80"]} total={300} defaultPageSize={20} current={1} />
                      <p>多语言分组示例：{window.lang.templateByUuid("P_YS_HR_HREM-FE_1591819943477248181")}</p>
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
