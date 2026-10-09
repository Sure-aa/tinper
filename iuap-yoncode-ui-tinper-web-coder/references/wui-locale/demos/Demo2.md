---
tags:
  - TinperNext
  - locale组件
---
# 多语 Locale

## 项目中使用，及切换语言

Locale组件通过context传递语言包，组件内部通过context获取语言包对象。

```tsx
import {Button, Locale, Popconfirm, EnUS, ZhCN, ZhTW} from '@tinper/next-ui';

import React, {Component} from 'react';

type PropType = {
	onChangeLang: React.MouseEventHandler<HTMLElement>;
	text: string;
};

const DemoButton = (props: PropType) => {
	return (
		<div style={{marginBottom: 20}}>
			<Button onClick={props.onChangeLang} colors="primary">
				{props.text}
			</Button>
		</div>
	)
}

let en = {
    ...EnUS,
    DemoButton: {
        text: 'Change Language'
    },
    PopconfirmContent: {
        content: 'Do you like tinper-next UI library?',
        buttonText: 'see right'
    }
};

let zh = {
    ...ZhCN,
    DemoButton: {
        text: '切换语言'
    },
    PopconfirmContent: {
        content: '你喜欢tinper-bee组件库吗？',
        buttonText: '看右边'
    }
};

let tw = {
    ...ZhTW,
    DemoButton: {
        text: '切換語言'
    },
    PopconfirmContent: {
        content: '你喜歡tinper-bee組件庫嗎？',
        buttonText: '看右邊'
    }
};


class Demo1 extends Component {
	state = {
	    lang: zh
	}
	handleChangeLang = () => {
	    const {lang} = this.state;
	    if (lang.lang === 'zh_CN') {
	        this.setState({
	            lang: tw
	        })
	    } else if (lang.lang === 'zh_TW') {
	        this.setState({
	            lang: en
	        })
	    } else {
	        this.setState({
	            lang: zh
	        })
	    }
	}

	render() {
	    const {lang} = this.state;

	    return (
	        <Locale locale={lang}>
	            <div>
	                <DemoButton
	                    onChangeLang={this.handleChangeLang}
	                    text={lang.DemoButton.text}
	                />
	                <Popconfirm
	                    trigger="click"
	                    placement="right"
	                    content={lang.PopconfirmContent.content}>
	                    <Button colors="primary">{lang.PopconfirmContent.buttonText}</Button>
	                </Popconfirm>
	            </div>

	        </Locale>
	    )
	}
}

export default Demo1;
```
