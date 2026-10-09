---
tags:
  - TinperNext
  - breadcrumb组件
---
# 面包屑 Breadcrumb

## 基础用法

Breadcrumb.Item定义子面包，`active`参数定义当前状态。

```tsx
import {Breadcrumb} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo1 extends Component {

	handleClick = (e: React.MouseEvent) => {
	    console.log(e.target);
	}

	render() {
	    return (
	        <Breadcrumb onClick={this.handleClick}>
	            <Breadcrumb.Item target="_blank" href="https://yondesign.yonyoucloud.com/website/#/tinpernext">
					Home
	            </Breadcrumb.Item>
	            <Breadcrumb.Item>
					Library
	            </Breadcrumb.Item>
	            <Breadcrumb.Item href="https://yondesign.yonyoucloud.com/website/#/tinpernext" active>
					Data
	            </Breadcrumb.Item>
	        </Breadcrumb>
	    )
	}
}

export default Demo1;
```
