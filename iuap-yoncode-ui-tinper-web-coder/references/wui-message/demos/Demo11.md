---
tags:
  - TinperNext
  - message组件
---
# 消息提醒 Message

## 控制是否显示图标

通过设置showIcon属性，控制是否显示图标
demo11

```tsx
import {Button, Message} from '@tinper/next-ui';
import React, {Component} from 'react';


const dark = function() {
    Message.destroy();
    Message.create({content: '显示图标的弹窗', color: "dark", duration: 3, showIcon: true});
};
const light = function() {
    Message.destroy();
    Message.create({content: '不显示图标的弹窗', color: "dark", duration: 3, showIcon: false});
};

class Demo1 extends Component {
    constructor(props: {}) {
        super(props);
    }

    render() {
        return (
            <div className="paddingDemo">
                <Button
                    colors="dark"
                    onClick={dark}>
					显示图标的弹窗
                </Button>
                <Button
                    shape="border"
                    onClick={light}>
					不显示图标的弹窗
                </Button>
            </div>
        )
    }
}


export default Demo1;
```
