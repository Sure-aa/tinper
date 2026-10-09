---
tags:
  - TinperNext
  - input组件
---
# 输入框 Input

## 浏览态

browser 开启浏览态。

```tsx
import {Input, Form, Radio, Button} from '@tinper/next-ui'
import React from 'react'

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

const options = [
    { label: 'xs', value: 'xs' },
    { label: 'sm', value: 'sm' },
    { label: 'md', value: 'md' },
    { label: 'nm', value: 'nm' },
    { label: 'lg', value: 'lg' },
];

const Demo15: React.FC = () => {
    const [browser, setBrowser] = React.useState(true)
    const [form] = Form.useForm()

    const onValuesChange = (changedValues: any, allValues: any) => {
        console.log('changedValues', changedValues);
        console.log('allValues', allValues);
    };
    return (
        <>
            <Button
                colors='primary'
                onClick={() => setBrowser(!browser)}
                style={{ marginLeft: '80px', marginBottom: '20px' }}
            >
                切换为{browser ? '编辑' : '浏览'}态
            </Button>
            <Form form={form} initialValues={{ name1: '文本内容', name2: '文本内容', name3: 'Textarea不限制行数。'.repeat(10), name4: '1234567', name6: 'Textarea限制行数。'.repeat(10) }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='切换size' name='name' >
                    <Radio.Group options={options} optionType="button" />
                </Form.Item>
                <Form.Item noStyle shouldUpdate={(prev, curr) => prev.name !== curr.name}>
                    {({ getFieldValue }: { getFieldValue: (name: string) => any }) => (
                        <>
                            <Form.Item {...formItemLayout} label='输入框下划线模式' name='name1' colon size={getFieldValue('name')}>
                                <Input browser={browser} bordered='bottom' size={getFieldValue('name')}/>
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='输入框带前后缀' name='name2' colon size={getFieldValue('name')}>
                                <Input browser={browser} prefix="前缀" suffix="后缀" size={getFieldValue('name')}/>
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='文本域显示模式' name='name3' colon size={getFieldValue('name')}>
                                <Input browser={browser} type='textarea' size={getFieldValue('name')}/>
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='文本域控制行数' name='name6' colon size={getFieldValue('name')}>
                                <Input browser={browser} type='textarea' size={getFieldValue('name')} autoSize={{ maxRows: 2 }}/>
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='密码框非显示模式' name='name4' colon size={getFieldValue('name')}>
                                <Input.Password browser={browser} size={getFieldValue('name')}/>
                            </Form.Item>
                        </>
                    )}
                </Form.Item>
            </Form>
        </>
    );
};

export default Demo15;
```
