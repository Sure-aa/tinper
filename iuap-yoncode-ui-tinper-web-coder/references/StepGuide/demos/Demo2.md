---
tags:
  - TinperNextPro
  - StepGuide组件
---
# StepGuide 步骤引导

## StepGuide使用，index 为可控状态
通过手动控制index，可以控制引导的流程，支持跨页面的引导

```jsx
import { useState } from "react";
import { StepGuide } from "tne-tinpernextpro-fe";
import { Button } from "@tinper/next-ui";

const Demo2 = () => {
    const [show, setShow] = useState(false);
    const [index, setIndex] = useState(0);
    const data = [
        {
            el: ".guide1-demo2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            callBack: (index, record) => {
                setIndex(index + 1);
            }
        },
        {
            el: ".guide2-demo2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            callBack: (index, record) => {
                setIndex(index + 1);
            }
        },
        {
            el: ".guide3-demo2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            callBack: (index, record) => {
                setIndex(index + 1);
            }
        },
        {
            el: ".guide4-demo2",
            title: "工作汇报升级了",
            content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
            callBack: (index, record) => {
                setIndex(index + 1);
            }
        },
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
                className="guide1-demo2"
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
                className="guide2-demo2"
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
                className="guide3-demo2"
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
                className="guide4-demo2"
            ></div>
            <StepGuide index={index} data={data} show={show} callBack={() => {
                alert(1);
                setShow(false);
            }}></StepGuide>
        </div>
    );
};

export default Demo2;
```
