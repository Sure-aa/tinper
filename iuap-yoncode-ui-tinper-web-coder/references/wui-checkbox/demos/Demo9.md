---
tags:
  - TinperNext
  - checkbox组件
---
# 多选 Checkbox

## 只读状态的复选框

设置readOnly属性，checkbox的按钮不可选中或取消

```tsx
import { Checkbox } from "@tinper/next-ui";
import React, { Component } from 'react';

const CheckboxGroup = Checkbox.Group;

// 复选框选项
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

interface Demo9State {
    basicValue: string[];
    colorValue: string[];
    dropdownValue2: string[];
}

class Demo9 extends Component<{}, Demo9State> {
    constructor(props: {}) {
        super(props);
        this.state = {
            basicValue: ['2', '3'],
            colorValue: ['primary', 'success', 'info', 'warning', 'danger', 'dark'],
            dropdownValue2: ['option1', 'option7']
        };
    }

    handleBasicChange = (value: string[]) => {
        this.setState({ basicValue: value });
    }

    handleColorChange = (value: string[]) => {
        this.setState({ colorValue: value });
    }

    handleDropdown2Change = (value: string[]) => {
        this.setState({ dropdownValue2: value });
    }

    render() {
        return (
            <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
                {/* 基础复选框组 */}
                <CheckboxGroup
                    value={this.state.basicValue}
                    readOnly
                    onChange={this.handleBasicChange}
                >
                    <Checkbox value='1'>选项1</Checkbox>
                    <Checkbox value='2'>选项2</Checkbox>
                    <Checkbox readOnly={false} value='3'>选项3</Checkbox>
                    <Checkbox value='4'>选项4</Checkbox>
                    <Checkbox value='5'>选项5</Checkbox>
                </CheckboxGroup>

                {/* 不同颜色的复选框 */}
                <CheckboxGroup readOnly value={this.state.colorValue} onChange={this.handleColorChange}>
                    <Checkbox value="primary" colors="primary">Primary</Checkbox>
                    <Checkbox value="success" colors="success" style={{ marginLeft: 8 }}>Success</Checkbox>
                    <Checkbox value="info" colors="info" style={{ marginLeft: 8 }}>Info</Checkbox>
                    <Checkbox value="warning" colors="warning" style={{ marginLeft: 8 }}>Warning</Checkbox>
                    <Checkbox value="danger" colors="danger" style={{ marginLeft: 8 }}>Danger</Checkbox>
                    <Checkbox value="dark" colors="dark" style={{ marginLeft: 8 }}>Dark</Checkbox>
                </CheckboxGroup>

                {/* 反色复选框 */}
                <div style={{display: 'flex', alignItems: 'center'}}>
                    <Checkbox value="primary" colors="primary" inverse checked readOnly>Primary反色</Checkbox>
                    <Checkbox value="success" colors="success" inverse checked readOnly style={{ marginLeft: 8 }}>Success反色</Checkbox>
                </div>

                {/* 下拉菜单 */}
                <CheckboxGroup
                    value={this.state.dropdownValue2}
                    onChange={this.handleDropdown2Change}
                    readOnly={true}
                    maxCount={true}
                    optionType="button"
                    options={opts}
                    style={{ width: '250px' }}
                />

                {/* 单独复选框和半选框 */}
                <div>
                    <Checkbox readOnly checked>独立复选框</Checkbox>
                    <Checkbox readOnly indeterminate style={{ marginLeft: 8 }}>只读半选框</Checkbox>
                </div>
            </div>
        );
    }
}

export default Demo9;
```
