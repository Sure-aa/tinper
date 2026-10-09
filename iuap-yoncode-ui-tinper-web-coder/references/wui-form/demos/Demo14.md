---
tags:
  - TinperNext
  - form组件
---
# 表单 Form

## labelCenter居中模式

labelCenter模式下，label文字上下居中（除单独设置labelSize的FormItem），详细描述见API文档

```tsx
import {
    Form,
    Input,
    Icon,
    Upload,
    ConfigProvider,
    Radio
} from '@tinper/next-ui';
import React from 'react';
import type {SizeType} from '../../../wui-core/src/types/iCore';

const formItemLayout = {
    labelCol: { span: 4 },
    wrapperCol: { span: 8 }
};

const normFile = (e: any) => {
    console.log('Upload event:', e);
    if (Array.isArray(e)) {
        return e;
    }
    return e && e.fileList;
};
const options = [
    { label: 'xs', value: 'xs' },
    { label: 'sm', value: 'sm' },
    { label: 'md', value: 'md' },
    { label: 'nm', value: 'nm' },
    { label: 'lg', value: 'lg' },
];
const Demo14 = () => {
    const [size, setSize] = React.useState<SizeType>('md');
    return (
        <>
            <Radio.Group value={size} options={options} optionType="button" defaultValue="md" onChange={(size: SizeType) => setSize(size)} style={{ marginLeft: '80px', marginBottom: '20px' }}/>
            <ConfigProvider size={size}>
                <Form
                    name='validate_other'
                    {...formItemLayout}
                    initialValues={{
                        date: '2021-05-15',
                    }}
                    labelCenter
                >

                    <Form.Item name='input' label='label文字较少场景' initialValue='小猪佩奇开心的一天' rules={[{ required: true }]}>
                        <Input requiredStyle />
                    </Form.Item>

                    <Form.Item name='input1' label='字显示超出两行场景文字显示超出两行场景文字显示超出两行场景文字显示超出两行场景文字显示超出两行场景' initialValue='小猪佩奇开心的一天' rules={[{ required: true }]} tooltip={'这是一个提示内容'}>
                        <Input requiredStyle />
                    </Form.Item>

                    <Form.Item
                        name='upload'
                        label='单独设置labelSize文字显示超出两行场景文字显示超出两行场景文字显示超出两行场景文字显示超出两行场景'
                        rules={[{ required: true }]}
                        tooltip={'这是一个提示内容'}
                        valuePropName='fileList'
                        getValueFromEvent={normFile}
                        labelSize={size}
                    >
                        <Upload listType='picture-card'>
                            <Icon type='uf-plus' style={{ fontSize: '22px' }} />
                            <p>上传</p>
                        </Upload>
                    </Form.Item>

                    <Form.Item label='单独设置labelSize' labelSize={size}>
                        <Input type='textarea' />
                    </Form.Item>
                </Form>
            </ConfigProvider>
        </>
    );
};
export default Demo14;
```
