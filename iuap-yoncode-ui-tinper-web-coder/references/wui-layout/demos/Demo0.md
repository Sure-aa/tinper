---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 基本结构

典型的页面布局(Layout,Header,Sider,Content,Footer) 使用fieldid

```tsx
import {Layout} from '@tinper/next-ui';
import React, {Component} from 'react';

const {Header, Content, Footer, Sider} = Layout;

class Demo5 extends Component {
    render() {
        return (
            <div className="layout-demo-basic">
                <Layout fieldid="layout">
                    <Header fieldid="header">Header</Header>
                    <Content fieldid="content">Content</Content>
                    <Footer fieldid="footer">Footer</Footer>
                </Layout>

                <Layout>
                    <Header>Header</Header>
                    <Layout>
                        <Sider>Sider</Sider>
                        <Content>Content</Content>
                    </Layout>
                    <Footer>Footer</Footer>
                </Layout>

                <Layout>
                    <Header>Header</Header>
                    <Layout>
                        <Content>Content</Content>
                        <Sider>Sider</Sider>
                    </Layout>
                    <Footer>Footer</Footer>
                </Layout>

                <Layout>
                    <Sider>Sider</Sider>
                    <Layout>
                        <Header>Header</Header>
                        <Content>Content</Content>
                        <Footer>Footer</Footer>
                    </Layout>
                </Layout>
            </div>
        )
    }
}

export default Demo5;
```

```css
.layout-demo-basic {
  text-align: center;

  > .wui-layout {
    margin-top: 35px;

    &:first-child {
      margin-top: 0;
    }
  }

  .wui-layout-header,
  .wui-layout-footer {
    color: #fff;
    background: #7dbcea;
  }

  .wui-layout-footer {
    line-height: 1.5;
  }

  .wui-layout-content {
    min-height: 120px;
    color: #fff;
    line-height: 120px;
    background: rgba(16, 142, 233, 1);
  }

  .wui-layout-sider {
    color: #fff;
    line-height: 120px;
    background: #3ba0e9;
  }
}
```
