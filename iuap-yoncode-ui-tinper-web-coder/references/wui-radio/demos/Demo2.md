---
tags:
  - TinperNext
  - radio组件
---
# 单选 Radio

## 不同颜色的radio

`color`参数控制背景色

```tsx
import { Radio, RadioGroupProps } from '@tinper/next-ui'
import React, { Component } from 'react'


class Demo2 extends Component<{}, { selectedValue: RadioGroupProps['value'] | undefined }> {
    constructor(props: {}) {
        super(props);
        this.state = {
            selectedValue: '3'
        };
    }

    handleChange: RadioGroupProps['onChange'] = (value, _e) => {
        this.setState({ selectedValue: value as Required<RadioGroupProps>['value'] });
    }

    render() {
        return (
            <>
                <span>默认模式：</span>
                <Radio.Group
                    name="color"
                    value={this.state.selectedValue}
                    onChange={this.handleChange}>
                    <Radio color="primary" value="1">苹果</Radio>
                    <Radio color="success" value="2">香蕉</Radio>
                    <Radio color="info" value="3">葡萄</Radio>
                    <Radio color="warning" value="4">菠萝</Radio>
                    <Radio color="danger" value="5">梨</Radio>
                    <Radio color="dark" value="6">石榴</Radio>
                </Radio.Group>
                <br />
                <br />
                <span>inverse 模式：</span>
                <Radio.Group
                    name="color"
                    value={this.state.selectedValue}
                    onChange={this.handleChange}>
                    <Radio color="primary" value="1" inverse>苹果</Radio>
                    <Radio color="success" value="2" inverse>香蕉</Radio>
                    <Radio color="info" value="3" inverse>葡萄</Radio>
                    <Radio color="warning" value="4" inverse>菠萝</Radio>
                    <Radio color="danger" value="5" inverse>梨</Radio>
                    <Radio color="dark" value="6" inverse>石榴</Radio>
                </Radio.Group>
            </>
        )
    }
}

export default Demo2;
```
