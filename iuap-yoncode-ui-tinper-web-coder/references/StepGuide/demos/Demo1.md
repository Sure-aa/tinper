---
tags:
  - TinperNextPro
  - StepGuide组件
---
# StepGuide 步骤引导

## StepGuide使用，定位元素进行引导
通过show属性可以控制展示。

```jsx
import { useState } from "react";
import { StepGuide } from "tne-tinpernextpro-fe";
import { Button } from "@tinper/next-ui";

const Demo1 = () => {
    const [show, setShow] = useState(false);
    const data = [
        {
            el: ".guide1",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        },
        {
            el: ".guide2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            callBack: (index, record) => {
                console.log("回调函数执行了=====", record);
            }
        },
        {
            el: ".guide3",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        },
        {
            el: ".guide4",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        },
        {
            el: ".guide5",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        },
        {
            el: ".guide6",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        },
        {
            el: ".guide7",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建"
        }
    ];
    // 展示引导
    function showDemo() {
        setShow(true);
    };
    return (
        <div style={{ position: "relative" , height: "700px"}}>
            <Button onClick={showDemo} type="primary">查看引导</Button>
            <div
                style={{
                    width: "50px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    left: "20px",
                    top: "30px"
                }}
                className="guide1"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    right: "20px",
                    top: "100px"
                }}
                className="guide2"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    right: "200px",
                    top: "200px"
                }}
                className="guide3"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    left: "200px",
                    top: "200px"
                }}
                className="guide4"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    left: "200px",
                    bottom: "50px"
                }}
                className="guide5"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    left: "500px",
                    bottom: "40px"
                }}
                className="guide6"
            ></div>
            <div
                style={{
                    width: "100px",
                    height: "100px",
                    background: "red",
                    position: "absolute",
                    left: "800px",
                    bottom: "70px"
                }}
                className="guide7"
            ></div>
            <StepGuide data={data} show={show} callBack={(type) => {
                alert(1);
                console.log('关闭类型', type)
                setShow(false);
            }}></StepGuide>
        </div>
    );
};

export default Demo1;
```
