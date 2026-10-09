---
tags:
  - TinperNextPro
  - Mobile组件
---
# Mobile 手机号

## 浏览态
browser 浏览态示例

```tsx
import React from "react";
import Mobile from "tne-tinpernextpro-fe/Mobile";
import { Button, Form } from "@tinper/next-ui";

const formItemLayout = {
    labelCol: {
        xs: { span: 1 },
        sm: { span: 1 }
    },
    wrapperCol: {
        xs: { span: 8 },
        sm: { span: 8 }
    }
};
const LayoutDemo = () => {
    const [browser, setBrowser] = React.useState(true);

    const onValuesChange = (changedValues: any, allValues: any) => {
        console.log(changedValues, allValues);
    };
    return (
        <>
            <Button  style={{ marginBottom: '10px' }} onClick={() => setBrowser(!browser)}>{browser ? '设置为编辑态' : '设置为浏览态'}</Button>

            <Form initialValues={{ name1: 1234567, name2: 7654321, name3: 1234567 }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='手机浏览态' name='name1' colon>
                    <Mobile browser={browser}></Mobile>
                </Form.Item>
                <Form.Item {...formItemLayout} label='下划线模式' name='name2' colon>
                    <Mobile browser={browser} bordered="bottom"></Mobile>
                </Form.Item>
                <Form.Item {...formItemLayout} label='无选项模式' name='name3' colon>
                    <Mobile browser={browser} bordered="bottom" hideCountryCode></Mobile>
                </Form.Item>
            </Form>
        </>
    );
};
export default LayoutDemo;
```

```less

```
