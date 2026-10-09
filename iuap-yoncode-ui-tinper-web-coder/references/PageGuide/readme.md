---
tags:
  - TinperNextPro
  - PageGuide组件
---
# PageGuide 页面引导

<!--PageGuide-->

## API

| 参数 | 说明 | 类型 | 默认值 | 版本 |
|--|--|--|--|--|
| data | 数据内容， 必填 | Object | {} | 1.0.9 |
| show | 是否展示 |  Boolean | false | 1.0.9 |
| callBack | 步骤完毕之后的回调 | Function | -- | 1.0.9 |
| gapTime  | 滚动间隔时间，以秒为单位 | Number | 8 | 1.0.9 |

### data示例
> data 参数接受一个对象，对象描述展示的卡片内容及数据
```jsx
const data = {
        title: "卡片标题", // 卡片标题
        guideList: [ // 每页滚动内容
        {
            desc: ( // 描述，支持文本或render函数
                <>
                    /**
                     * reactNode ，支持render函数
                    */
                </>
            ),
            img: require("./images/P1@2x_zh-CN.png"), // 图片
        },
        {   desc: "新增附言等....", 
            img: require("./images/P2@2x_zh-CN.png") 
        },
    ]
}
```
