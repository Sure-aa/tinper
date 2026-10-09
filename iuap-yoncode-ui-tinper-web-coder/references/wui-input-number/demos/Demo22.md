---
tags:
  - TinperNext
  - inputnumber组件
---
# 数字框 InputNumber

## 只读态

readOnly属性为true时触发的状态，不可交互

```tsx
import React from 'react';
import { InputNumber } from '@tinper/next-ui';

const Demo22: React.FC = () => {
    return (
        <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
            {/* 全边框示例 */}
            <InputNumber
                placeholder="普通数字输入框"
                defaultValue="1234.56"
                readOnly={true}
                style={{ width: 200 }}
            />

            {/* 底边框示例 */}
            <InputNumber
                placeholder="底部边框"
                bordered="bottom"
                defaultValue="2345.67"
                readOnly={true}
                style={{ width: 200 }}
            />

            {/* 无边框示例 */}
            <InputNumber
                placeholder="无边框"
                bordered={false}
                defaultValue="3456.78"
                readOnly={true}
                style={{ width: 200 }}
            />

            {/* 带前后缀示例 */}
            <InputNumber
                addonBefore={<span style={{ fontSize: '13px' }}>￥</span>}
                addonAfter={<span style={{ fontSize: '13px' }}>元</span>}
                defaultValue="5678.90"
                readOnly={true}
                style={{ width: 200 }}
            />
        </div>
    );
};

export default Demo22;
```
