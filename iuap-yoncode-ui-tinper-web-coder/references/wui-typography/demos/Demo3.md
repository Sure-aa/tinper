---
tags:
  - TinperNext
  - typography组件
---
# 排版 Typography

## Typography 其他属性

示例包含Typography.Paragraph disabled

```tsx
import {
    Typography
} from '@tinper/next-ui';
import React from 'react';

const defaultConfig = {
    rows: 2, // div 高度模拟为100，相应的row 缩小为0.2，行高则计算为100 * 0.2 = 20
    ellipsisStr: "...",
    ellipsis: true,
    showPopover: true,
    direction: "end",
    expandable: true,
    defaultExpanded: true,
};
let defaultText = `A design is a plan or specification for the construction of an object or system or for the
  implementation of an activity or process. A design is a plan or specification for the
  construction of an object or system or for the implementation of an activity or process. A design is a plan or specification for the construction of an object or system or for the
  implementation of an activity or process. A design is a plan or specification for the
  construction of an object or system or for the implementation of an activity or process.`;
const Demo3 = () => {
    // const onExpand = (isExpand: boolean) => {
    //     console.log('isExpand', isExpand)
    // }
    return (
        <div style={{ width: "200px", position: "relative" }}>
            <Typography.Paragraph
                className="demo-ellipsis"
                ellipsis={{
                    ...defaultConfig,
                }}
            >
                {defaultText}
            </Typography.Paragraph>
        </div>
    );
};

export default Demo3;
```
