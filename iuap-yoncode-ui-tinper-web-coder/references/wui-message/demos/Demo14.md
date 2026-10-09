---
tags:
  - TinperNext
  - message组件
---
# 消息提醒 Message

## 可折叠示例

返回大串代码时，需要将代码隐藏，并且显示友好的提示，被隐藏的代码需要通过展开进行查看、复制

```tsx
import {Button, Message, Icon, Clipboard} from '@tinper/next-ui';
import React, {Component} from 'react';

const receiveContent = " traceld:c444c71f94e9ef13\n "
                    + "timestamp:2022-11-17 21:26:51\n "
                    + "userld:4be9794-ec5f-4e4d-b37f-fb89c8e5eff\n "
                    + "tenantld:0000KPC165PABLPTS60000\n "
                    + "eMessage:QuerySchemaExecutor error,entity uri \n "
                    + "exceptionAtack:com.yonyou.ucf.mdd.ext.da0.meta.crud.Q\n "
                    + "          at com.yonyou.ucf.mdd.ext.dao.meta.cru\n "
                    + "          at com.yonyou.ucf.mdd.ext.dao.meta.cru\n "
                    + "          at com.yonyou.ucf.mdd.ext.dao.meta.cru "
class ErrorContent extends Component<{}, {show: boolean, copyShow: boolean}> {
    timer: ReturnType<typeof setTimeout> | null = null;
    constructor(props: {}) {
        super(props);
        this.state = {
            show: false,
            copyShow: false
        }
    }
    setCopyShow = () => {
        this.setState({ copyShow: true })
        this.timer = setTimeout((() => this.setState({ copyShow: false })), 2000)
    }
    componentWillUnmount() {
        if (this.timer) {
            clearTimeout(this.timer);
            this.timer = null;
        }
    }
    render() {
        const { show, copyShow } = this.state;
        return (
            <div>
                抱歉，系统出了点小问题，请联系支持人员
                <div className="description-error-content">
                    {show ?
                        <div className="receive-content">
                            <pre>{receiveContent}</pre>
                        </div> : null}
                    <Clipboard action="copy" text={receiveContent} className='copy' success={this.setCopyShow}>复制代码</Clipboard>
                    <span className="describe" onClick={() => this.setState({show: !show})}>
                        错误详情
                        {show ? <Icon type="uf-arrow-up" /> : <Icon type="uf-arrow-down" />}
                    </span>
                    {copyShow ?
                        <div className="successCopy">复制成功</div> : null
                    }
                </div>
            </div>
        )
    }
}

const danger = function() {
    Message.destroy();
    Message.create({content: <ErrorContent />, color: 'danger', duration: null});
};
class Demo14 extends Component {
    constructor(props: {}) {
        super(props);
    }

    render() {
        return (
            <div className="paddingDemo">
                <Button bordered onClick={danger}>详情折叠事例</Button>
            </div>
        )
    }
}


export default Demo14;
```

```css
.description-error-content{
    margin-top: 16px;
    margin-bottom: 10px;
    overflow: hidden;
  
    span, .copy{
      float: right;
      width: 48px;
      height: 18px;
      font-family: PingFangSC-Regular;
      font-size: 12px;
      color: #0033CC;
      line-height: 18px;
      cursor: pointer;
    }
    .describe{
      width: 75px;
      margin-right: 16px;
  
      .uf{
        font-size: 12px;
      }
    }
    .receive-content pre{
      font-family: PingFangSC-Regular;
      font-size: 12px;
      color: #666666;
      line-height: 18px;
      margin-top: 0;
    }
    .successCopy {
      position: absolute;
      top: calc(50% - 15px);
      left: calc(50% - 44px);
      width: 88px;
      height: 30px;
      font-size: 14px;
      color: #FFFFFF;
      background: #505766;
      border-radius: 4px;
      text-align: center;
      line-height: 30px;
    }
}
```
