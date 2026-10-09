---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 上-中-下 布局

最基本的『上-中-下』布局

```tsx
import {Breadcrumb, Layout, Menu} from '@tinper/next-ui';
import React, {Component} from 'react';

const {Header, Content, Footer} = Layout;

class Demo6 extends Component {
    render() {
        return (
            <Layout className="layout">
                <Header>
                    <Menu theme="dark" mode="horizontal" defaultSelectedKeys={['2']}>
                        <Menu.Item key="1">nav 1</Menu.Item>
                        <Menu.Item key="2">nav 2</Menu.Item>
                        <Menu.Item key="3">nav 3</Menu.Item>
                    </Menu>
                </Header>
                <Content style={{padding: '0 50px', background: '#f5f5f5'}}>
                    <Breadcrumb style={{margin: '16px 0'}}>
                        <Breadcrumb.Item>Home</Breadcrumb.Item>
                        <Breadcrumb.Item>List</Breadcrumb.Item>
                        <Breadcrumb.Item>App</Breadcrumb.Item>
                    </Breadcrumb>
                    <div className="site-layout-content">Content</div>
                </Content>
                <Footer style={{textAlign: 'center', background: '#f5f5f5'}}>用友网络科技股份有限公司@next-ui</Footer>
            </Layout>
        )
    }
}

export default Demo6;
```

```css
.site-layout-content {
  min-height: 280px;
  padding: 24px;
  background: #fff;
}

.layout {
  .wui-menu-horizontal {
    line-height: 64px;
  }
}
```
