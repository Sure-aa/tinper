---
tags:
  - TinperNext
  - select组件
---
# 下拉框 Select

## option包含副标题

option 内容可以自定义，输入框的值可使用optionLabelProp指定回填

```tsx
import {Select, SelectValue} from "@tinper/next-ui";
import React, {Component} from "react";

const Option = Select.Option;

const data = [
    { title: '按方法结算', describe: '通过专项成本方法计算转出成本金额' },
    { title: '按内容结算', describe: '通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额成本金，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额成本金' },
    { title: '按明细结算', describe: '根据实际投入成本明细维护转出成本金额' },
]

class Demo extends Component {
    handleChange = (value: SelectValue) => {
	    console.log(value);
    };

    render() {
        return (
            <div>
                <Select onChange={this.handleChange} dropdownClassName="custom-options" optionLabelProp="key" defaultValue="按方法结算" style={{ width: 400 }}>
                    {
                        data.map(item => (
                            <Option key={item.title} title={item.describe}>
                                <h3>{item.title}</h3>
                                <span>{item.describe}</span>
                            </Option>
                        ))
                    }
                </Select>
            </div>
        );
    }
}

export default Demo;
```

```css
.custom-options .wui-select-item-option-content{
    h3{
        font-size: 12px;
        font-weight: 400;
        color: #333333;
        line-height: 18px;
        margin: 0 0 5px 0;
    }
    span{
        font-size: 12px;
        color: #999999;
        line-height: 18px;
        white-space: break-spaces;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-box-orient: vertical;  // 不建议使用
        -webkit-line-clamp: 3;
        overflow: hidden;
        // 使用组件库内部 注册的css变量 整体风格保持一致
        color: var(--wui-select-color-text-tertiary);
        font-size: var(--wui-select-font-size-tertiary);
        font-weight: var(--wui-select-font-weight-tertiary);
    }
}
```
