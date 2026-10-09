---
tags:
  - TinperNext
  - progress组件
---
# 进度条 Progress

## 自定义进度条渐变色

linear-gradient 的封装。推荐只传两种颜色。

```tsx
import {Progress} from "@tinper/next-ui";
import React, {Component} from 'react';

class Demo11 extends Component {
    render() {
        return (
            <div>
                <Progress
                    strokeColor={{
                        '0%': '#108ee9',
                        '100%': '#87d068',
                    }}
                    percent={99.9}
                />
                <Progress
                    strokeColor={{
                        from: '#108ee9',
                        to: '#87d068',
                    }}
                    percent={99.9}
                    status="active"
                />
                <Progress
                    type="circle"
                    strokeColor={{
                        '0%': '#108ee9',
                        '100%': '#87d068',
                    }}
                    percent={90}
                />
                <Progress
                    type="circle"
                    strokeColor={{
                        '0%': '#108ee9',
                        '100%': '#87d068',
                    }}
                    percent={100}
                />
            </div>
        )
    }
}

export default Demo11
```
