---
tags:
  - TinperNext
  - colorpicker组件
---
# 取色器 ColorPicker

## 取色板

提供预制色板的取色板组件(包含fieldid)

```tsx
import {ColorPicker} from '@tinper/next-ui';
import React, {Component} from 'react';

class Demo1 extends Component <{}, {value:string}> {
	state = {
	    value: "#E14C46"
	}

	Change = (v:{class: string; rgba: string; hex: string;}) => {
	    console.log("选择的色彩信息 ：", v);
	    this.setState({
	        value: '#ffffff'
	    })
	}

	render() {
	    return (
	        <ColorPicker onChange={this.Change} value={this.state.value}/>
	    )
	}
}

export default Demo1
```
