---
tags:
  - TinperNext
  - colorpicker组件
---
# 取色器 ColorPicker

## 设置必输项

`required`参数设置是否必填

```tsx
import {ColorPicker} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo2 extends Component <{}, {value:string}> {
	state = {
	    value: "#E14C46"
	}

	handleChange = (v:{class: string; rgba: string; hex: string;}) => {
	    console.log("选择的色彩信息 ：", v);
	    this.setState({
	        value: v.hex || ''
	    })
	}

	render() {
	    return (
	        <ColorPicker
	            className="demo2"
	            placeholder="请输入十六进制色值"
	            value={this.state.value}
	            onChange={this.handleChange}
	            label="颜色"
	            required={true}
	            disabledAlpha={true}
	        />
	    )
	}
}

export default Demo2
```
