---
tags:
  - TinperNext
  - cascader组件
---
# 级联菜单 Cascader

## 为空时显示的内容

notFoundContent属性，当下拉列表为空时显示的内容。

```tsx
import {Cascader, Col, Row, CascaderProps} from '@tinper/next-ui';
import React, {Component} from 'react';


const options: any[] = [];

class Demo17 extends Component {

	onChange: CascaderProps['onChange'] = (value, selectedOptions) => {
	    console.log(value, selectedOptions);
	}

	render() {
	    return (
	        <Row>
	            <Col md={4}>
	                <div className="height-150">
	                    <Cascader
	                        //  defaultValue={defaultOptions}
	                        options={options}
	                        onChange={this.onChange}
	                        placeholder="请选择"
	                        //  separator = " > "
	                        notFoundContent='下拉为空时的显示'
	                    />
	                </div>
	            </Col>
	        </Row>
	    )
	}
}

export default Demo17;
```
