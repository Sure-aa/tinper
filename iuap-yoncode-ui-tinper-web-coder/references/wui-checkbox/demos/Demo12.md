---
tags:
  - TinperNext
  - checkbox组件
---
# 多选 Checkbox

## 浏览态

browser 开启浏览态。

```tsx
import { Checkbox, Button, Form } from "@tinper/next-ui";
import React, { useState } from 'react';

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
    {label: 'Apple', value: '1'},
    {label: 'Pear', value: '2'},
    {label: 'Orange', value: '3'},
];

const Demo12: React.FC = () => {
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
            <Form initialValues={{ name1: ['2', '3'], name2: ['1', '3'], name3: ['2', '4'] }} onValuesChange={onValuesChange}>
                <Form.Item {...formItemLayout} label='多选带下划线模式' name='name1' colon>
                    <Checkbox.Group browser={browser} bordered='bottom'>
                        <Checkbox value='1'>
                            First
                        </Checkbox>
                        <Checkbox value='2'>
                            Second
                        </Checkbox>
                        <Checkbox value='3'>
                            Third
                        </Checkbox>
                        <Checkbox value='4'>
                            Fourth
                        </Checkbox>
                        <Checkbox value='5'>
                            Fifth
                        </Checkbox>
                    </Checkbox.Group>
                </Form.Item>
                <Form.Item {...formItemLayout} label='多选按钮模式' name='name2' colon>
                    <Checkbox.Group browser={browser} optionType="button" options={options} />
                </Form.Item>
                <Form.Item {...formItemLayout} label='多选平铺显示模式' name='name3' colon>
                    <Checkbox.Group browser={browser} browserShow options={options} />
                </Form.Item>
                <Form.Item {...formItemLayout} label='单个多选框' name='name4' colon>
                    <Checkbox browser={browser}>Fifth</Checkbox>
                </Form.Item>
            </Form>
        </>
    );
};

export default Demo12;
```
