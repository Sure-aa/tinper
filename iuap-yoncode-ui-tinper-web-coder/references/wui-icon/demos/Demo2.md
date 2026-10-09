---
tags:
  - TinperNext
  - icon组件
---
# 图标 Icon

## icon 角度旋转

可以将图标自定义旋转

```tsx
import {Icon} from "@tinper/next-ui";
import React, {Component} from 'react';


class Demo1 extends Component {
    render() {
        return (
            <div>
                <Icon type="uf-xiayitiao-copy" style={{fontSize: '36px'}} fieldid="test" />
                <Icon type="uf-xiayitiao-copy" style={{fontSize: '36px'}} rotate={90}/>
            </div>
        )
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
