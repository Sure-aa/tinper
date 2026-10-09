---
tags:
  - TinperNext
  - icon组件
---
# 图标 Icon

## Icon 图标

使用 <Icon /> 标签声明组件，指定图标对应的 type 属性。

```tsx
import {Icon, Message} from "@tinper/next-ui";

import copy from "copy-to-clipboard";
import React, {Component} from "react";
import iconJson from '../../../../packages/wui-core/scss/iconfont.json'

class Demo1 extends Component {

    componentDidMount() {
        document.getElementById("icon_lists")?.addEventListener("click", this.copyCode);
    }

    componentWillUnmount() {
        document.getElementById("icon_lists")?.removeEventListener('click', this.copyCode);
    }

	copyCode = (e: MouseEvent) => {
	    let iconCls = e.target && this.findIconCls(e.target);
	    if (!iconCls) return;
	    let code = `<Icon type="${iconCls}" />`;
	    copy(code);
	    Message.destroy();
	    Message.success({
	        content: (
	            <div>
	                <span className="code-cont">{code}</span> copied
	            </div>
	        ),
	    });
	};
	findIconCls = (target: any) => {
	    target.nodeName.toLowerCase() == "li" ||
		target.parentNode!.nodeName.toLowerCase() == "li";
	    let iconCls = "";
	    if (target.nodeName.toLowerCase() == "li") {
	        iconCls = target.lastElementChild!.innerText;
	        return iconCls && iconCls.substr(1);
	    } else if (target.parentNode!.nodeName.toLowerCase() == "li") {
	        iconCls = target.parentNode!.lastElementChild.innerText;
	        return iconCls && iconCls.substr(1);
	    }
	    return iconCls;
	};

	render() {
	    return (
	        <div className="tinper-icon-demo">
	            <ul id="icon_lists" className="icon_lists">
	                {iconJson.glyphs.map((icon: any) => {
	                    return (
	                        <li key={icon.icon_id}>
	                            <Icon type={`${iconJson.css_prefix_text}${icon.font_class}`} />
	                            <div className="name">{icon.name}</div>
	                            <div className="fontclass">{`.${iconJson.css_prefix_text}${icon.font_class}`}</div>
	                        </li>
	                    )
	                })}
	            </ul>
	        </div>
	    );
	}
}

export default Demo1;
```

```css
.icon_lists:after {
  clear: both;
  display: block;
  visibility: hidden;
  content: '.';
}

.icon_lists li {
  position: relative;
  float: left;
  width: 10.66%;
  height: 108px;
  margin: 4px 0;
  padding: 10px 0 0;
  overflow: hidden;
  color: #555;
  text-align: center;
  list-style: none;
  background-color: #fff;
  border-radius: 4px;
  cursor: pointer;
  -webkit-transition: color 0.3s ease-in-out, background-color 0.3s ease-in-out;
  transition: color 0.3s ease-in-out, background-color 0.3s ease-in-out;

  .uf {
    display: block;
    font-size: 36px;
    line-height: 36px;
    margin: 12px 0 8px;
    color: #555;
    -webkit-transition: color 0.3s ease-in-out, transform 0.3s ease-in-out;
    -moz-transition: color 0.3s ease-in-out, transform 0.3s ease-in-out;
    transition: color 0.3s ease-in-out, transform 0.3s ease-in-out;
  }

  &:hover {
    color: #fff;
    background-color: #505766;

    .uf {
      color: #fff;
      -webkit-transform: scale(1.4);
      -ms-transform: scale(1.4);
      transform: scale(1.4);
    }
  }

  .name, .fontclass {
    white-space: nowrap;
    text-align: center;
    line-height: 18px;
    -webkit-transform: scale(0.83);
    -ms-transform: scale(0.83);
    transform: scale(0.83);
  }
}

.wui-message-notice {
  margin-bottom: 12px;
  font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace;

  .code-cont {
    background: #ddd;
    display: inline-block;
    border-radius: 3px;
    line-height: 18px;
  }
}
```
