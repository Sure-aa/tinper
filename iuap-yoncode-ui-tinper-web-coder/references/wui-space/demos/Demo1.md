---
tags:
  - TinperNext
  - space组件
---
# 间距 Space

## 对齐

设置对齐模式。

```tsx
import {Button, Space} from "@tinper/next-ui";
import React, {Component} from "react";

class Demo1 extends Component {

    render() {
	    return (
	        <div className="space-align-container">
	            <div className="space-align-block">
	                <Space align="center">
						center
	                    <Button type="primary">Primary</Button>
	                    <span className="mock-block">Block</span>
	                </Space>
	            </div>
	            <div className="space-align-block">
	                <Space align="start">
						start
	                    <Button type="primary">Primary</Button>
	                    <span className="mock-block">Block</span>
	                </Space>
	            </div>
	            <div className="space-align-block">
	                <Space align="end">
						end
	                    <Button type="primary">Primary</Button>
	                    <span className="mock-block">Block</span>
	                </Space>
	            </div>
	            <div className="space-align-block">
	                <Space align="baseline">
						baseline
	                    <Button type="primary">Primary</Button>
	                    <span className="mock-block">Block</span>
	                </Space>
	            </div>
	        </div>
	    );
    }
}

export default Demo1;
```

```css
.space-align-container {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
}

.space-align-block {
  flex: none;
  margin: 8px 4px;
  padding: 4px;
  border: 1px solid #40a9ff;
}

.space-align-block .mock-block {
  display: inline-block;
  padding: 32px 8px 16px;
  background: rgba(150, 150, 150, 0.2);
}
```
