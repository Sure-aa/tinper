---
tags:
  - TinperNext
  - message组件
---
# 消息提醒 Message

## 使用fieldid

使用fieldid。

```tsx
import {Button, Message} from '@tinper/next-ui';
import React, {Component} from 'react';


const onClick = function() {
    Message.destroy();
    Message.create({content: <div>单据提交成功</div>, color: "light", fieldid: "demo"});
};

class Demo12 extends Component {
    constructor(props: {}) {
        super(props);
    }

    render() {
        return (
            <div className="paddingDemo">
                <Button
                    shape="border"
                    onClick={onClick}>
					消息
                </Button>
            </div>
        )
    }
}


export default Demo12;
```
