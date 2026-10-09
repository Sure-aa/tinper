---
tags:
  - TinperNextPro
  - PageGuide组件
---
# PageGuide 页面引导

## PageGuide使用，定位轮播图式引导
通过show属性可以控制展示。

```jsx
import React, { useState } from "react";
import { PageGuide } from 'tne-tinpernextpro-fe';
import { Button, ConfigProvider, Radio, Space } from "@tinper/next-ui";

const Demo1 = () => {
    const [show, setShow] = useState(false);
    const [dir, setDir] = React.useState('ltr');    
    const data = {
        title: "审批意见升级了",
        guideList: [
            {
                desc: (
                    <>
                        <span style={{ color: "red" }}>谢谢小星星</span>xxxxxx{" "}
                        <a href="xxx">
                            了解更多
                        </a>
                    </>
                ),
                img: require("./images/P1@2x_zh-CN.png")
            },
            { desc: "新增附言等....", img: require("./images/P2@2x_zh-CN.png") },
            { desc: "新增附言等....", img: require("./images/P3@2x_zh-CN.png") },
            { desc: "新增附言等....", img: require("./images/P4@2x_zh-CN.png") }
        ]
    };

    // 展示引导
    function showDemo() {
        setShow(true);
    };
    return (
        <>
            <Space className={"demo-wrap--list--buttons"}>
                布局方向:
                <Radio.Group value={dir} onChange={value => setDir(value)}>
                    <Radio value="ltr" inverse>LTR</Radio>
                    <Radio value="rtl" inverse>RTL</Radio>
                </Radio.Group>
            </Space>
        
            <ConfigProvider dir={dir}>
                <div style={{ position: "relative", height: "700px" }}>
                        <Button onClick={showDemo} type="primary">查看引导</Button>
                        <PageGuide data={data} show={show} callBack={() => {
                                alert(1)
                                setShow(false);
                            }} gapTime={2}></PageGuide>
                </div>
            </ConfigProvider>
        </>
    );
};

export default Demo1;
```
