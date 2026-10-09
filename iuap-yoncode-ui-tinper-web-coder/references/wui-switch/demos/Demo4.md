---
tags:
  - TinperNext
  - switch组件
---
# 开关 Switch

## 开关只读禁用状态

```tsx
import {Button, Col, Row, Switch} from '@tinper/next-ui';
import React, {Component} from "react";

interface SwitchState {
	defaultDisabled: boolean;
}

class Demo4 extends Component<{}, SwitchState> {
    constructor(props: {}) {
        super(props);
        this.state = {
            defaultDisabled: true
        };
    }

	onChange = () => {
	    this.setState({
	        defaultDisabled: !this.state.defaultDisabled
	    });
	};

	render() {
	    return (
	        <Row>
	            <Col sm={2}>
	                只读态开关：
	            </Col>
	            <Col sm={2}>
	                <Switch className="switch" readOnly={this.state.defaultDisabled}/>
	            </Col>
	            <Col sm={2}>
	                禁用态开关：
	            </Col>
	            <Col sm={2}>
	                <Switch className="switch" disabled={this.state.defaultDisabled}/>
	            </Col>
	            <Col sm={2}>
	                <Button onClick={this.onChange}>toggle</Button>
	            </Col>
	        </Row>
	    );
	}
}

export default Demo4;
```
