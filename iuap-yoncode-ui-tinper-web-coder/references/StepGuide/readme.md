---
tags:
  - TinperNextPro
  - StepGuide组件
---
# StepGuide 步骤引导

<!--StepGuide-->

## API

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|--|--|--|--|--|
| data | 数据内容， 必填 | Array | [] | 1.0.9 |
| show | 是否展示 |  Boolean | false | 1.0.9 |
| callBack | 步骤完毕之后的回调 | Function | -- | 1.0.9 |
| index | 当前步骤数据的下标 | number | -- | 15.2.x |

### data API
| 参数 | 说明 | 类型 | 默认值 | 版本 |
|--|--|--|--|--|
| el | 标识引导要定位的元素的选择器 | string | -- | 1.0.9 |
| title | 引导的标题内容 | ReactNode | -- | 1.0.9 |
| content | 引导的内容说明 | ReactNode | -- | 1.0.9 |
| callBack | 当前步骤完毕之后的回调，一般用于index可控场景 | Function | -- | 1.0.9 |
| crossPage | 跨页面引导回调，例如() => {this.props.history.push('/cloud/detail')}，非必需，仅在需要跳转页面的步骤配置 | Function | -- | 1.0.9 |
| direction | 提示弹出的方向: leftCenter rightCenter center | string | -- | 15.2.x |

### data示例
> data 参数接受一个数组，步骤会根据数组的内容index进行执行，el为标识引导要定位的元素的选择器，接受querySelector可以接受的选择器。
```js
const data = [
    {  // 第一步 
        el: ".guide1", // 要定位到的元素
        title: "工作汇报升级了", // 弹窗引导的标题内容
        content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建", // 引导的内容说明
        callBack: (index, record) => void() // 点击下一步之后的回调 非必需
    },
    {   // 第二步 
        el: ".guide2",
        title: "工作汇报升级了",
        content: "您可以点击这里进入写汇报页面， 也可以通Opt N 完成创建",
        callBack: (index, record) => void()
    }
]
```
