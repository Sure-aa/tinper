---
tags:
  - TinperNext
  - calendar组件
---
# 日历 Calendar

## 自定义日期属性

getDateCellAttr

```tsx
import {Calendar} from "@tinper/next-ui";
import {Moment} from "moment"
import React, {Component} from 'react';

function onSelect(value: Moment) {
    console.log(value);
}


class Demo7 extends Component {
	getDateCellAttr = (_current: Moment, _value: Moment) => {
	    return {
	        aaa: '111',
	        title: '222'
	    }
	}

	render() {
	    return (
	        <div>
	            <Calendar
	                onSelect={onSelect}
	                fullscreen
	                getDateCellAttr={this.getDateCellAttr}
	            />
	        </div>
	    )
	}
}


export default Demo7
```
