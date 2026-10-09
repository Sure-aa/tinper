---
tags:
  - TinperNext
  - input组件
---
# 输入框 Input

## 只读态

readOnly属性为true时触发的状态

```tsx
import React from 'react';
import { Input } from '@tinper/next-ui';

const Demo16: React.FC = () => {
    return (
        <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
            {/* 全边框输入框 */}
            <Input
                placeholder="普通输入框（只读状态）"
                defaultValue="这是普通输入框的内容"
                readOnly={true}
            />

            {/* 带前后缀的输入框 */}
            <Input
                prefix="￥"
                suffix="元"
                placeholder="带前后缀（只读状态）"
                defaultValue="1234.56"
                readOnly={true}
            />

            {/* 底边框输入框 */}
            <Input
                placeholder="只显示底部边框（只读状态）"
                defaultValue="底边框输入框的示例内容"
                bordered="bottom"
                readOnly={true}
            />

            {/* 无边框输入框 */}
            <Input
                placeholder="无边框输入框（只读状态）"
                defaultValue="无边框输入框的示例内容"
                bordered={false}
                readOnly={true}
            />
            {/* 搜索框示例 */}
            <Input.Search
                placeholder="搜索内容"
                defaultValue="搜索示例内容"
                readOnly={true}
            />
            {/* 密码框示例 */}
            <Input
                type="password"
                placeholder="请输入密码"
                defaultValue="password123"
                readOnly={true}
            />
            {/* 多行文本示例 */}
            <Input.TextArea
                placeholder="请输入多行文本"
                defaultValue="这是一段只读状态的多行文本内容示例。&#10;第二行内容示例。"
                readOnly={true}
                autoSize={{ minRows: 4, maxRows: 6 }}
            />
        </div>
    );
};

export default Demo16;
```
