---
tags:
  - TinperNextPro
  - StepGuide组件
---
# StepGuide 步骤引导

## 指定提示弹出方向
当弹框上下空间不足时，可以指定弹出方向rightCenter, leftCenter, center

```jsx
import { useState } from "react";
import { StepGuide } from "tne-tinpernextpro-fe";
import { Button, Layout, Menu, Icon } from "@tinper/next-ui";

const { Header, Content, Sider } = Layout;

const Demo3 = () => {
    const [show, setShow] = useState(false);
    const [collapsed, setCollapsed] = useState(false);
    const data = [
        {
            el: ".guide1",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            direction: "rightCenter"
        },
        {
            el: ".guide2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
        },
        {
            el: ".guide3",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            direction: "center"
        }
    ];
    // 展示引导
    function showDemo() {
        setShow(true);
    };
    return (
        <div style={{ position: "relative" , height: "700px"}}>
            <Button onClick={showDemo} type="primary" style={{ marginBottom: '10px' }}>查看引导</Button>
            <Layout className="layout-triger">
	            <Sider className="guide1" theme='dark' trigger={null} collapsible collapsed={collapsed}>
	                <div className="logo"/>
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
	                <Header className="guide2 site-layout-background" style={{ padding: 0 }}>
	                    <span className="trigger" onClick={() => setCollapsed(!collapsed)}>
                            {collapsed ? <Icon type="uf-2arrow-right"/> : <Icon type="uf-2arrow-left"/>}
                        </span>
	                </Header>
	                <Content className="guide3 site-layout-background" style={{
                        margin: '24px 16px',
                        padding: 24,
                        minHeight: 280,
                    }}>
						Content
	                </Content>
	            </Layout>
	        </Layout>
            <StepGuide data={data} show={show} callBack={(type) => {
                alert(1);
                setShow(false);
            }}></StepGuide>
        </div>
    );
};

export default Demo3;
```

```less
.demos-wui-layout {
    .layout-triger .trigger {
      padding: 0 24px;
      font-size: 18px;
      line-height: 64px;
      cursor: pointer;
      transition: color 0.3s;
    }
  
    .layout-triger .trigger:hover {
      color: #1890ff;
    }
  
    .layout-triger .logo {
      height: 32px;
      width: calc(100% - 32px);
      margin: 16px;
      background: rgba(255, 255, 255, 0.3);
      box-sizing: border-box;
    }
  
    .layout-triger .site-layout {
      background: #f0f2f5;
  
      main {
        margin: 24px 16px;
        padding: 24px;
      }
    }
  
    .site-layout .site-layout-background {
      background: #fff;
    }
  }
```
