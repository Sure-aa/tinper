---
tags:
  - TinperNext
  - input组件
---
# 输入框 Input

## onLinkClick

当为只读或浏览态时，设置`onLinkClick`属性， 文字会渲染成可点击状态，点击触发`onLinkClick`函数

```tsx
import React from 'react'
import Input from '../../src'

/**
 * 测试 onLinkClick 功能
 * 在 readOnly 和 browser 状态下，当有值时显示为可点击的蓝色文字
 * 点击时触发回调并传递当前值
 */
const Demo17 = () => {

    const handleonLinkClick = (value: string | number) => {
        console.log(`触发回调，值为: ${value}`)
    }

    const handleBrowseronLinkClick = (value: string | number) => {
        console.log(`浏览态触发回调，值为: ${value}`)
    }

    return (
        <div>
            <div style={{ marginBottom: '20px' }}>
                <h4>1. 普通状态（不触发）</h4>
                <Input
                    value="普通输入框内容"
                    onLinkClick={handleonLinkClick}
                    placeholder="普通状态不会触发 onLinkClick"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>2. 只读状态 - 有值（可点击）</h4>
                <Input
                    readOnly
                    type="search"
                    value="点击我触发回调"
                    onLinkClick={handleonLinkClick}
                    placeholder="只读状态"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>3. 只读状态 - 无值（不可点击）</h4>
                <Input
                    readOnly
                    value=""
                    onLinkClick={handleonLinkClick}
                    placeholder="无值时不可点击"
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>4. 浏览态 - 有值（可点击）</h4>
                <Input
                    browser
                    value="浏览态可点击内容"
                    onLinkClick={handleBrowseronLinkClick}
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>5. 浏览态 - 无值（不可点击）</h4>
                <Input
                    browser
                    value=""
                    onLinkClick={handleBrowseronLinkClick}
                />
            </div>

            <div style={{ marginBottom: '20px' }}>
                <h4>7. 没有 onLinkClick 的只读状态（普通只读）</h4>
                <Input
                    readOnly
                    value="普通只读内容"
                    placeholder="没有回调函数"
                />
            </div>
        </div>
    )
}

export default Demo17
```
