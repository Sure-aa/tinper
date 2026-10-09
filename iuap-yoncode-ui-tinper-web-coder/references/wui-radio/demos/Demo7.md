---
tags:
  - TinperNext
  - radio组件
---
# 单选 Radio

## fieldid用法

传递fieldid属性，生成fieldid dom属性

```tsx
import {Radio, RadioGroupProps} from '@tinper/next-ui'
import React, {Component} from 'react'

class Demo7 extends Component <{}, {value: RadioGroupProps['value']}> {
    constructor(props:{}) {
        super(props)
        this.state = {
            value: ''
        }
    }

    handleChange: RadioGroupProps['onChange'] = (value) => {
        this.setState({value: value as RadioGroupProps['value']});
    }
    render() {
        return (
            <div className="demo7">
                <Radio.Group onChange={this.handleChange} value={this.state.value}>
                    <Radio value="1" fieldid="loki">苹果</Radio>
                </Radio.Group>
            </div>
        )
    }
}

export default Demo7;
```
