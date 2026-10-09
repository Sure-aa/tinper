---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

## 浏览态支持传size
根据当前size设置尺寸

```tsx
import React from "react";
import { ProConfigProvider } from "tne-tinpernextpro-fe";
import { Radio } from '@tinper/next-ui';
import { Email, Phone, Identity, InputMultilang } from "tne-tinpernextpro-fe";
import Mobile from "tne-tinpernextpro-fe/Mobile";

const options = [
  { label: 'xs', value: 'xs' },
  { label: 'sm', value: 'sm' },
  { label: 'md', value: 'md' },
  { label: 'nm', value: 'nm' },
  { label: 'lg', value: 'lg' },
];
const LayoutDemo = () => {
  const [val, setVal] = React.useState("hello123");
  const [size, setSize] = React.useState<any>('md');

  return (
    <>
      <Radio.Group value={size} options={options} optionType="button" defaultValue="md" onChange={(size: any) => setSize(size)} style={{ marginBottom: '20px' }} />
      <ProConfigProvider size={size} browser>
        {
          (config) => {
            return <>
              <Email value={val} onChange={(val: any) => setVal(val)} fieldid="email-test" placeholder="请输入" ></Email>
              <br />
              <Phone fieldid="phone-test" value={{ H: "123", E: "9999" }} />
              <br />
              <Identity fieldid="identity-test" value={{ identity: '412702111111111000', idType: '1' }} />
              <br />
              <Mobile fieldid="mobile-test" value="12345678901"/>
              <br />
              <InputMultilang
                placeholder="请输入"
                modalProps={{
                  centered: true,
                }}
                localeList={{
                  'zh_CN': '一只小花狗',
                  'en_US': 'litle dog',
                }}
                isPopConfirm={false}
                locale="zh_CN"
                status="browser"
              />
            </>
          }
        }
      </ProConfigProvider>
    </>
  );
};
export default LayoutDemo;
```
