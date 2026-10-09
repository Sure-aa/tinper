---
tags:
  - TinperNextPro
  - Email组件
---
# Email 邮箱

## 浏览态
browser 设置浏览态。

```tsx
import React from "react";
import { Email } from "tne-tinpernextpro-fe";
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
            <Button style={{ marginBottom: '10px' }} onClick={() => setBrowser(!browser)}>{browser ? '设置为编辑态' : '设置为浏览态'}</Button>

            <Form initialValues={{ name1: 'hello123@yonyou.com', name2: 'hello123@163.com' }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='邮箱浏览态' name='name1' colon>
                    <Email browser={browser} placeholder="请输入"></Email>
                </Form.Item>
                <Form.Item {...formItemLayout} label='下划线模式' name='name2' colon>
                    <Email browser={browser} placeholder="请输入" bordered="bottom"></Email>
                </Form.Item>
            </Form>
        </>
    );
};
export default LayoutDemo;
```
