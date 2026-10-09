---
tags:
  - TinperNext
  - radio组件
---
# 单选 Radio

## 只读状态的单选框

设置readOnly属性，radio的状态不能改变。RadioGroup下的Radio的readOnly属性无效，使用父节点的readOnly。

```tsx
import React, { Component } from 'react';
import { Radio } from '@tinper/next-ui';

// 按钮选项
const btns = [
    <Radio.Button key="1" color="primary" value="1">选项一</Radio.Button>,
    <Radio.Button key="2" color="success" value="2">选项二</Radio.Button>,
    <Radio.Button key="3" color="info" value="3">选项三</Radio.Button>,
    <Radio.Button key="4" color="warning" value="4">选项四</Radio.Button>,
    <Radio.Button key="5" color="danger" value="5">选项五</Radio.Button>,
    <Radio.Button key="6" color="dark" value="6">选项六</Radio.Button>,
    <Radio.Button key="7" color="primary" value="7">选项七</Radio.Button>,
    <Radio.Button key="8" color="success" value="8">选项八</Radio.Button>,
];

// 普通选项
const opts = [
    { label: '选项一', value: 'option1' },
    { label: '选项二', value: 'option2' },
    { label: '选项三', value: 'option3' },
    { label: '选项四', value: 'option4' },
    { label: '选项五', value: 'option5' },
    { label: '选项六', value: 'option6' },
    { label: '选项七', value: 'option7' },
    { label: '选项八', value: 'option8' },
];

interface Demo8State {
    basicValue: string;
    buttonValue: string;
    dropdownValue1: string;
    dropdownValue2: string;
}

class Demo8 extends Component<{}, Demo8State> {
    constructor(props: {}) {
        super(props);
        this.state = {
            basicValue: '2',
            buttonValue: '2',
            dropdownValue1: '2',
            dropdownValue2: 'option2'
        };
    }

    handleChange = (value: string) => {
        this.setState({ basicValue: value });
    }

    handleButtonChange = (value: string) => {
        this.setState({ buttonValue: value });
    }

    handleDropdown1Change = (value: string) => {
        this.setState({ dropdownValue1: value });
    }

    handleDropdown2Change = (value: string) => {
        this.setState({ dropdownValue2: value });
    }

    render() {
        return (
            <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
                {/* 基础单选组 - 展示已选/未选状态 */}
                <Radio.Group
                    value={this.state.basicValue}
                    onChange={this.handleChange}
                    readOnly={true}
                >
                    <Radio value="1">未选项</Radio>
                    <Radio value="2">已选项</Radio>
                    <Radio value="3">未选项</Radio>
                </Radio.Group>

                {/* 不同颜色的单选框 */}
                <Radio.Group readOnly={true}>
                    <Radio value="primary" color="primary" checked>Primary</Radio>
                    <Radio value="success" color="success" checked style={{ marginLeft: 8 }}>Success</Radio>
                    <Radio value="info" color="info" checked style={{ marginLeft: 8 }}>Info</Radio>
                    <Radio value="warning" color="warning" checked style={{ marginLeft: 8 }}>Warning</Radio>
                    <Radio value="danger" color="danger" checked style={{ marginLeft: 8 }}>Danger</Radio>
                    <Radio value="dark" color="dark" checked style={{ marginLeft: 8 }}>Dark</Radio>
                </Radio.Group>

                {/* 反色单选框 */}
                <Radio.Group readOnly={true}>
                    <Radio value="primary" color="primary" inverse checked>Primary反色</Radio>
                    <Radio value="success" color="success" inverse checked style={{ marginLeft: 8 }}>Success反色</Radio>
                </Radio.Group>

                {/* 下拉菜单形式一：按钮溢出显示更多 */}
                <div style={{ width: '250px' }}>
                    <Radio.Group
                        value={this.state.dropdownValue1}
                        onChange={this.handleDropdown1Change}
                        readOnly={true}
                        maxCount={true}
                        showMoreText
                        size="sm"
                    >
                        {btns}
                    </Radio.Group>
                </div>

                {/* 下拉菜单形式二：底部展开式 */}
                <div style={{ width: '250px' }}>
                    <Radio.Group
                        value={this.state.dropdownValue2}
                        onChange={this.handleDropdown2Change}
                        readOnly={true}
                        maxCount={true}
                        tiled
                        optionType="button"
                        showMoreText
                        options={opts}
                    />
                </div>
            </div>
        );
    }
}

export default Demo8;
```
