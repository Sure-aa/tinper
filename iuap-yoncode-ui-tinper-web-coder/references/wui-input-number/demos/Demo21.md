---
tags:
  - TinperNext
  - inputnumber组件
---
# 数字框 InputNumber

## 浏览态

browser 浏览态示例

```tsx
import {InputNumber, Form, Radio} from '@tinper/next-ui'
import React from 'react'
const InputNumberGroup = InputNumber.InputNumberGroup;

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
const Demo21: React.FC = () => {
    const [form] = Form.useForm()
    const onValuesChange = (changedValues: any, allValues: any) => {
        console.log('changedValues', changedValues);
        console.log('allValues', allValues);
    };
    return (
        <>
            <Form form={form} initialValues={{
                name: 'md',
                name0: 123,
                name1: null,
                name2: 5,
                name3: 123456789,
                name4: 123456789,
                name5: 123456789,
                name6: 123456789,
                name7: [123, 456]
            }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='切换size' name='name' >
                    <Radio.Group options={options} optionType="button" />
                </Form.Item>
                <Form.Item noStyle shouldUpdate={(prev, curr) => prev.name !== curr.name}>
                    {({ getFieldValue }: { getFieldValue: (name: string) => any }) => (
                        <>
                            <Form.Item {...formItemLayout} label='基础模式' name='name0' size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" bordered='bottom' size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='显示空值' name='name1' size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='带格式场景' name='name2' colon size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle='one' format={(value: string | number) => `${value} %`} size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='显示数量级' name='name3' colon size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" showMark size={getFieldValue('name')}/>
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='显示前后缀' name='name4' colon size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" addonBefore='宽' addonAfter='米' size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='金额大写上下布局' name='name5' colon size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" showAmountInWords inputWidth="100%" bordered='bottom' size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='金额大写左右布局' name='name6' colon size={getFieldValue('name')}>
                                <InputNumber browser={true} iconStyle="one" showAmountInWords showAmountLayout='horizontal' bordered='bottom' size={getFieldValue('name')} />
                            </Form.Item>
                            <Form.Item {...formItemLayout} label='InputNumberGroup' name='name7' colon size={getFieldValue('name')}>
                                <InputNumberGroup
                                    browser={true}
                                    iconStyle='double'
                                    bordered='bottom'
                                    size={getFieldValue('name')}
                                />
                            </Form.Item>
                        </>
                    )}
                </Form.Item>
            </Form>
        </>
    );
};

export default Demo21;
```
