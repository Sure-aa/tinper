---
tags:
  - TinperNextPro
  - Identity组件
---
# Identity 证件号

## 浏览态
browser 浏览态示例。

```tsx
import React from "react";
import { Identity } from "tne-tinpernextpro-fe";
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

            <Form initialValues={{ name1: { identity: '412702111111111000', idType: '1' }, name2: { identity: 'G12345678', idType: '3' }, name3: { identity: 'G12345678'} }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='证件浏览态' name='name1' colon>
                    <Identity browser={browser} ></Identity>
                </Form.Item>
                <Form.Item {...formItemLayout} label='下划线模式' name='name2' colon>
                    <Identity browser={browser} bordered="bottom"></Identity>
                </Form.Item>
                <Form.Item {...formItemLayout} label='无选项模式' name='name3' colon>
                    <Identity browser={browser} bordered="bottom" showSelect={false}></Identity>
                </Form.Item>
            </Form>
        </>
    );
};
export default LayoutDemo;
```
