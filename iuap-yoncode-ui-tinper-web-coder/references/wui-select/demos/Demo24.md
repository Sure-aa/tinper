---
tags:
  - TinperNext
  - select组件
---
# 下拉框 Select

## 下拉浏览态和只读态

设置browser为浏览态样式, 浏览态内容最多展示两行，超出省略号展示；设置readOnly为只读态，可操作查看但不可更改值

```tsx
import {Select, Radio} from "@tinper/next-ui";
import React, {Component} from "react";

const {Option} = Select;

const ComponentChildren: React.ReactNode[] = [];
for (let i = 10; i < 300; i++) {
    ComponentChildren.push(<Option value={i.toString()}>{i}</Option>);
}

const options = [
    { label: 'auto', value: 'auto' },
    { label: 'responsive', value: 'responsive' },
];

class Demo24 extends Component {
    state = {
        maxTagCount: 'responsive'
    }

    handleMaxTagCountChange = (checkedValues: string) => {
        this.setState({
            maxTagCount: checkedValues
        })
    }

    render() {
        return (
            <>
                <h4>浏览态</h4>
                <Select
                    mode='multiple'
                    browserStyle={{width: 320}}
                    defaultValue={['china', 'russia']}
                    browser={true}
                >
                    <Option value="china" label="China">
					    China (中国)<span>*</span>
                    </Option>
                    <Option value="russia" label="Russia">
					    Russia (俄罗斯)
                    </Option>
                    <Option value="australia" label="Australia">
					    Australia (澳大利亚)
                    </Option>
                    <Option value="korea" label="Korea">
					    Korea (韩国)
                    </Option>
                </Select>
                <br/>
                <Select
                    mode='multiple'
                    browserStyle={{width: 320}}
                    defaultValue={['china', 'russia']}
                    browser={true}
                    bordered="bottom"
                    optionLabelProp="label"
                >
                    <Option value="china" label="China">
					    China (中国)<span>*</span>
                    </Option>
                    <Option value="russia" label="Russia">
                        Russia (俄罗斯)
                    </Option>
                    <Option value="australia" label="Australia">
					    Australia (澳大利亚)
                    </Option>
                    <Option value="korea" label="Korea">
					    Korea (韩国)
                    </Option>
                </Select>
                <h4>只读态</h4>
                <div style={{marginBottom: 10, display: 'flex'}}>maxTagCount： <Radio.Group optionType="button" options={options} value={this.state.maxTagCount} onChange={this.handleMaxTagCountChange}/> </div>
                <Select
                    mode="multiple"
                    style={{width: 425}}
                    placeholder="请选择"
                    allowClear
                    value={['10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31', '32', '33', '34', '35']}
                    readOnly
                    maxTagCount={this.state.maxTagCount as 'auto' | 'responsive'}
                >
                    {ComponentChildren}
                </Select>
                <br/>
                <br/>
                <Select
                    mode="multiple"
                    style={{width: 425}}
                    placeholder="请选择"
                    allowClear
                    value={['10', '11', '12', '13', '14', '15']}
                    readOnly
                    maxTagCount={this.state.maxTagCount as 'auto' | 'responsive'}
                    requiredStyle
                >
                    {ComponentChildren}
                </Select>
                <br/>
                <br/>
                <Select
                    allowClear
                    defaultValue="all"
                    style={{width: 200}}
                    readOnly
                    bordered="bottom"
                >
                    <Option value="all">全部</Option>
                    <Option value="confirming">待确认</Option>
                    <Option value="executing">执行中</Option>
                    <Option value="completed"> 已办结</Option>
                    <Option value="termination">终止</Option>
                </Select>
            </>
        )
    }
}

export default Demo24;
```
