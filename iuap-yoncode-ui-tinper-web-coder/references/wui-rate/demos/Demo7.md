---
tags:
  - TinperNext
  - rate组件
---
# 评分 Rate

## style属性

自定义样式对象

```tsx
import {Rate} from "@tinper/next-ui";
import React, {Component} from 'react';

interface RateState {
	value: number;
}
class Demo1 extends Component<{}, RateState> {
    constructor(props: {}) {
        super(props);
        this.state = {
            value: 3
        };
    }

	handChange = (value: number) => {
	    this.setState({
	        value
	    })
	}

	render() {
	    return (
	        <Rate style={{color: 'red'}} value={this.state.value} allowHalf onChange={this.handChange}/>
	    )
	}
}

export default Demo1;
```
