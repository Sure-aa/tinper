---
tags:
  - TinperNext
  - switch组件
---
# 开关 Switch

## 浏览态示例

browser 开启浏览态。

```tsx
import { Switch, Form } from '@tinper/next-ui';
import React, { Component } from "react";

const formItemLayout = {
    labelCol: {
        xs: { span: 2 },
        sm: { span: 2 }
    },
    wrapperCol: {
        xs: { span: 8 },
        sm: { span: 8 }
    }
};
class Demo6 extends Component<any, any> {

    render() {
        return (
            <>
                <Form>
                    <Form.Item {...formItemLayout} label='浏览态默认关闭' name='name1' colon>
                        <Switch browser />
                    </Form.Item>
                    <Form.Item {...formItemLayout} label='浏览态默认开启' name='name2' colon>
                        <Switch browser checked={true}/>
                    </Form.Item>
                    <Form.Item {...formItemLayout} label='设置浏览态文字' name='name3' colon>
                        <Switch browser checked={true} browserText="**abc**" />
                    </Form.Item>
                </Form>
            </>
        );
    }
}

export default Demo6;
```
