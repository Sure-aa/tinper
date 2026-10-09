---
tags:
  - TinperNext
  - layout组件
---
# 栅格布局 Layout

## 侧边栏收起结合拖拽分割器使用

使用Spliter分割器进行拖拽，结合侧边栏收起功能,添加resizerable={false}禁止拖拽

```tsx
import { Icon, Layout, Menu } from '@tinper/next-ui';
import React, { Component } from 'react';
import './Demo10.scss';

const { Header, Content, Sider } = Layout;

class Demo10 extends Component {
    state={
        width: 200
    }

    onCollapse = (collapsed: boolean) => {
        console.log('onCollapse', collapsed);
        this.setState({
            width: collapsed ? 0 : 200
        })
    }

    render() {
        return (
            <Layout className="layout-spliter" style={{ height: '395px'}}>
                <Sider collapsible collapsedWidth={0} onCollapse={this.onCollapse} width={this.state.width} theme='dark'>
                    <div className="logo" />
                    <Menu theme="dark" mode="inline" defaultSelectedKeys={['1']}>
                        <Menu.Item key="1">
                                nav 1
                        </Menu.Item>
                        <Menu.Item key="2">
                                nav 2
                        </Menu.Item>
                        <Menu.Item key="3">
                                nav 3
                        </Menu.Item>
                    </Menu>
                </Sider>
                <Layout className="site-layout">
                    <Header>
                        <Icon type="uf-home" />
                    </Header>
                    <Content
                        style={{
                            margin: '24px 16px',
                            padding: 24,
                            minHeight: 280,
                        }}
                    >
                        <p>content..........</p>
                        <p>content..........</p>
                        <p>content..........</p>
                    </Content>
                </Layout>
            </Layout>
        )
    }
}

export default Demo10;
```

```css
.layout-spliter{
      box-shadow: 0 2px 3px rgb(0 0 0 / 10%);
      .site-layout{
          header{
              line-height: 64px;
              padding-left: 20px;
              border-bottom: 1px solid #f1f1f1;
              .uf{
                  font-size: 20px;
              }
          }
      }
      .wui-layout-sider {
          padding: 16px 0;
          .logo {
              height: 32px;
              width: calc(100% - 32px);
              margin: 0 16px 30px 16px;
              background: rgba(255, 255, 255, 0.3);
              box-sizing: border-box;
          }
      }
  }
```
