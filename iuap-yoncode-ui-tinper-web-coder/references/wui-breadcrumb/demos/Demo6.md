---
tags:
  - TinperNext
  - breadcrumb组件
---
# 面包屑 Breadcrumb

## 自适应父节点宽度

fillSpace = true 面包屑会自适应父节点宽度，超出内容下拉展示

```tsx
import {Breadcrumb, Menu} from "@tinper/next-ui";
import React, {Component} from 'react';

const {Item} = Menu;

class Demo6 extends Component {

     handleClick = (e: React.MouseEvent) => {
         console.log(e.target);
     }

     render() {

         const menu = (
             <Menu>
                 <Item key="1">借款合同</Item>
                 <Item key="2">抵/质押合同</Item>
                 <Item key="3">担保合同</Item>
             </Menu>
         );

         const itemList = ["Home", "Library", "Library_1", "Library_2", "data_1", "data_2", "data_3", "page_1", "验证长文字超出最大宽度需要显示省略号", "page_3", "page_4"]

         return (
             <div style={{ width: '60%'}}>
                 <Breadcrumb fillSpace style={{height: 100}} onClick={this.handleClick}>
                     {itemList.map((item, _index) =>
                         <Breadcrumb.Item
                             overlay={item === 'Library' ? menu : undefined}
                             active={item === 'page_4'} href={item === 'Home' ? "https://yondesign.yonyoucloud.com/website/#/tinpernext" : undefined}
                             key={item}
                         >
                             {item}
                         </Breadcrumb.Item>)
                     }
                 </Breadcrumb>
             </div>
         )
     }
}

export default Demo6;
```
