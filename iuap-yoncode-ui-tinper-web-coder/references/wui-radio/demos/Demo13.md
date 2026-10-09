---
tags:
  - TinperNext
  - radio组件
---
# 单选 Radio

## 浏览态

browser 开启浏览态。

```tsx
import { Radio, Button, Form } from '@tinper/next-ui'
import React, { useState } from 'react'

const options = [
    { label: 'Apple', value: 'Apple' },
    { label: 'Pear', value: 'Pear' },
    { label: 'Orange', value: 'Orange'},
];
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
const Demo13: React.FC = () => {
    const [browser, setBroswer] = useState<any>(true);
    const onValuesChange = (changedValues: any, allValues: any) => {
        console.log('changedValues', changedValues);
        console.log('allValues', allValues);
    };
    return (
        <>
            <Button
                onClick={() => setBroswer(!browser)}
                style={{ marginLeft: '20px', marginBottom: '10px' }}
            >
                切换为{browser ? '编辑' : '浏览'}态
            </Button>
            <Form initialValues={{ name1: 'Apple', name2: 'Pear', name3: 'Orange' }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='单选带下划线模式' name='name1' colon>
                    <Radio.Group browser={browser} options={options} bordered='bottom'/>
                </Form.Item>
                <Form.Item {...formItemLayout} label='单选按钮模式' name='name2' colon>
                    <Radio.Group browser={browser} options={options} optionType="button" />
                </Form.Item>
                <Form.Item {...formItemLayout} label='单选平铺显示模式' name='name3' colon>
                    <Radio.Group browserShow browser={browser} options={options} />
                </Form.Item>
                <Form.Item {...formItemLayout} label='单个单选框模式' name='name4' colon>
                    <Radio browser={browser}>Apple</Radio>
                </Form.Item>
            </Form>
        </>
    );
};

export default Demo13;
```
