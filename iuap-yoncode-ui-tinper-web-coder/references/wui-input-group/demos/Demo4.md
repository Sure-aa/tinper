---
tags:
  - TinperNext
  - inputgroup组件
---
# 输入框组 InputGroup

## 只读态

实际上inputGroup没有自己的只读态，它的只读基于input组件,它的前后缀是用户自定义的

```tsx
import React from 'react';
import { Input, Icon } from '@tinper/next-ui';

const Demo4: React.FC = () => {
    return (
        <div style={{display: 'grid', gridTemplateColumns: 'repeat(1, 1fr)', gridGap: '10px'}}>
            {/* 基本输入组 */}
            <Input.Group>
                <Input.Group.Addon
                    style={{
                        backgroundColor: 'rgb(247, 247, 247)',
                        borderColor: 'rgba(80, 87, 102, 0.2)',
                        cursor: 'default',
                        pointerEvents: 'none',
                        fontSize: '13px',
                    }}
                >
                    项目
                </Input.Group.Addon>
                <Input
                    readOnly={true}
                    defaultValue="企业财务系统"
                    prefix={<Icon type="uf-pencil" />}
                    suffix={<Icon type="uf-search" />}
                />
            </Input.Group>

            {/* 货币输入组 */}
            <Input.Group>
                <Input.Group.Addon
                    style={{
                        backgroundColor: 'rgb(247, 247, 247)',
                        borderColor: 'rgba(80, 87, 102, 0.2)',
                        cursor: 'default',
                        pointerEvents: 'none',
                        fontSize: '13px',
                    }}>￥
                </Input.Group.Addon>
                <Input
                    readOnly={true}
                    defaultValue="10,000"
                    suffix="元"
                />
            </Input.Group>

            {/* 密码输入组 */}
            <Input.Group>
                <Input.Group.Addon
                    style={{
                        backgroundColor: 'rgb(247, 247, 247)',
                        borderColor: 'rgba(80, 87, 102, 0.2)',
                        cursor: 'default',
                        pointerEvents: 'none',
                        fontSize: '13px',
                    }}>密码
                </Input.Group.Addon>
                <Input
                    type="password"
                    readOnly={true}
                    defaultValue="password123"
                    suffix={<Icon type="uf-eye" />}
                />
            </Input.Group>

            {/* 底边框输入组 */}
            <Input.Group bordered="bottom">
                <Input.Group.Addon
                    style={{
                        borderBottomColor: 'rgba(80, 87, 102, 0.2)',
                        cursor: 'default',
                        pointerEvents: 'none',
                        fontSize: '13px',
                    }}>邮箱
                </Input.Group.Addon>
                <Input
                    bordered="bottom"
                    readOnly={true}
                    defaultValue="example@mail.com"
                    suffix="@mail.com"
                />
            </Input.Group>

            {/* 无边框输入组 */}
            <Input.Group bordered={false}>
                <Input.Group.Addon
                    style={{
                        backgroundColor: 'rgb(247, 247, 247)',
                        cursor: 'default',
                        pointerEvents: 'none',
                        fontSize: '13px',
                    }}>用户
                </Input.Group.Addon>
                <Input
                    bordered={false}
                    readOnly={true}
                    defaultValue="admin"
                    prefix={<Icon type="uf-user" />}
                />
            </Input.Group>
        </div>
    );
};

export default Demo4;
```
