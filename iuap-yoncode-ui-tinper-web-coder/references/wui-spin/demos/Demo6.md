---
tags:
  - TinperNext
  - spin组件
---
# 加载提示 Spin

## 自定义加载图标

如需自定义加载图标，需要同时设置 `loadingType` 属性和 `indicator` 属性。

```tsx
import {Spin} from '@tinper/next-ui';
import React, {Component} from 'react';

let imgsrc = "http://design.yonyoucloud.com/static/bee.tinper.org-demo/Spin.gif";

interface SpinState {
	show: boolean;
}
class Demo6 extends Component<{}, SpinState> {
    constructor(props: {}) {
        super(props);
        this.state = {
            show: true
        }
    }


    render() {
        const beeIcon = <img src={imgsrc} style={{width: '50px'}}/>;
        return (
            <div className="demo5" id="demo5">
                <Spin
                    getPopupContainer={() => document.getElementById('demo5')}
                    spinning={this.state.show}
                    indicator={beeIcon} // 自定义图标的内容
                />
            </div>
        )
    }
}


export default Demo6;
```
