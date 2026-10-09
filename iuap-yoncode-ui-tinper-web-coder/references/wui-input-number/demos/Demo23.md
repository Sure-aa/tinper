---
tags:
  - TinperNext
  - inputnumber组件
---
# 数字框 InputNumber

## onLinkClick

当为只读或浏览态时，设置`onLinkClick`属性， 文字会渲染成可点击状态，点击触发`onLinkClick`函数

```tsx
import React from 'react'
import { InputNumber } from '@tinper/next-ui';

/**
 * 测试 onLinkClick 功能
 * 在 readOnly 和 browser 状态下，当有值时显示为可点击的蓝色文字
 * 点击时触发回调并传递当前值
 */
const Demo23 = () => {

    const handleonLinkClick = (value: string | number) => {
        console.log(`触发回调，值为: ${value}`)
    }

    const handleBrowseronLinkClick = (value: string | number) => {
        console.log(`浏览态触发回调，值为: ${value}`)
    }

    return (
        <div style={{ width: '200px' }}>
            <div style={{ marginBottom: '20px' }}>
                <h4>1. 普通状态（不触发）</h4>
                <InputNumber
                    defaultValue={123}
                    onLinkClick={handleonLinkClick}
                    placeholder="普通状态不会触发 onLinkClick"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>2. 只读状态 - 有值（可点击）</h4>
                <InputNumber
                    readOnly
                    defaultValue={123}
                    onLinkClick={handleonLinkClick}
                    placeholder="只读状态"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>3. 只读状态 - 无值（不可点击）</h4>
                <InputNumber
                    readOnly
                    defaultValue=""
                    onLinkClick={handleonLinkClick}
                    placeholder="无值时不可点击"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>4. 浏览态 - 有值（可点击）</h4>
                <InputNumber
                    browser
                    defaultValue={123}
                    onLinkClick={handleBrowseronLinkClick}
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>5. 浏览态 - 无值（不可点击）</h4>
                <InputNumber
                    browser
                    defaultValue=""
                    onLinkClick={handleBrowseronLinkClick}
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>7. 没有 onLinkClick 的只读状态（普通只读）</h4>
                <InputNumber
                    readOnly
                    defaultValue={123}
                    placeholder="没有回调函数"
                />
            </div>
        </div>
    )
}

export default Demo23
```
