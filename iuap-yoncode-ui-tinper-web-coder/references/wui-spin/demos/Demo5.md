---
tags:
  - TinperNext
  - spin组件
---
# 加载提示 Spin

## 不同尺寸的Spin

通过设置`size`属性，来控制Spin图标的大小

```tsx
import {Spin} from '@tinper/next-ui';
import React, {Component} from 'react';

interface SpinState {
	show: boolean;
}
class Demo5 extends Component<{}, SpinState> {
    containerRef: HTMLDivElement | null;
    constructor(props: {}) {
        super(props);
        this.state = {
            show: true
        }
        this.containerRef = null;
    }


    render() {
        return (
            <div className="demo5" ref={ref => this.containerRef = ref} style={{position: 'relative'}}>
                <Spin size="sm" getPopupContainer={() => this.containerRef} spinning={this.state.show} loadingType="rotate"/>
                <Spin getPopupContainer={() => this.containerRef} spinning={this.state.show} loadingType="rotate"/>
                <Spin size="lg" getPopupContainer={() => this.containerRef} spinning={this.state.show} loadingType="rotate"/>
            </div>
        )
    }
}


export default Demo5;
```
