---
tags:
  - TinperNextPro
  - Phone组件
---
# Phone 电话号

## 浏览态
browser 浏览态使用。

```tsx
import React from "react";
import { Phone } from "tne-tinpernextpro-fe";
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

            <Form initialValues={{ name1: { H: '12345', E: "" }, name2: { H: '12345', E: "67890" }, name3: { H: '12345', E: "" } }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='电话浏览态' name='name1' colon>
                    <Phone browser={browser}></Phone>
                </Form.Item>
                <Form.Item {...formItemLayout} label='下划线模式' name='name2' colon>
                    <Phone browser={browser} bordered="bottom" noExtension={false}></Phone>
                </Form.Item>
                <Form.Item {...formItemLayout} label='无选项模式' name='name3' colon>
                    <Phone browser={browser} bordered="bottom" hideCityCode></Phone>
                </Form.Item>
            </Form>
        </>
    );
};
export default LayoutDemo;
```
