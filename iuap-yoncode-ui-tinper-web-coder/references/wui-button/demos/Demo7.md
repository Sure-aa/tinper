---
tags:
  - TinperNext
  - button组件
---
# 按钮 Button

## fieldid

给loading或者由组件生成的icon添加fieldid属性。

```tsx
import React, { Component } from 'react';
import { Button, Icon } from "@tinper/next-ui";

class Demo7 extends Component {

    render() {
        return (
            <div className="demoPadding">
                <Button colors="primary" icon='uf-search' fieldid={'field-btn'} id={'btn'} />
                <Button colors="primary" icon='uf-search' fieldid={'field-btn_1'} loading />
                <Button colors="primary" fieldid={'plus'} id={'plus'} icon={<Icon type="uf-plus"/>}>新增</Button>
                <Button size='lg' bordered={false} icon={<Icon type="uf-plus" />}
                    style={{display: 'flex', justifyContent: 'center', border: 'none', flexDirection: 'column', alignItems: 'center', height: '60px'}}>新增</Button>
            </div>
        )
    }
}

export default Demo7;
```

```css
.demoPadding {
  button {
    margin: auto 5px;
  }

  .divider {
    margin: 6px 0;
    height: 1px;
    overflow: hidden;
    background-color: #fff;
  }
}

.el-icon--right {
  margin-left: 4px;
}
```
