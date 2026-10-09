---
tags:
  - TinperNext
  - dropdown组件
---
# 下拉按钮 Dropdown

## children中传递内容 代替overlay

仅Dropdown.Button支持使用children作为下拉，只有此种情况可不传overlay

```tsx
import { Dropdown, Menu, MenuProps} from '@tinper/next-ui';
import React, {Component} from 'react';


const {Item} = Menu;

const dataList = [
    {"key": "1", value: "借款合同", id: "a"},
    {"key": "2", value: "抵/质押合同", id: "v"},
    {"key": "3", value: "担保合同", id: "c"},
    {"key": "4", value: "联保合同", id: "d"},
]

function onVisibleChange(visible: boolean) {
    console.log(visible);
}

class Demo12 extends Component {

    /**
	 * 获取当前选中行的item对象。
	 * @param {*} value
	 */
    onSelect: MenuProps['onSelect'] = ({key, domEvent}) => {
        console.log(`${key} selected`); // 获取key
    }

    render() {
        const menu1 = (
            <Menu onSelect={this.onSelect}>{
                dataList.map(da => <Item key={da.key} data-da={JSON.stringify(da)}>{da.value}</Item>)}
            </Menu>)

        return (
            <div className="demoPadding">
                <Dropdown.Button
                    trigger={['click']}
                    // overlay={menu1}
                    getPopupContainer={dom => dom}
                    onVisibleChange={onVisibleChange}>
                    点击显示
                    {menu1}
                </Dropdown.Button>
            </div>
        )
    }
}

export default Demo12;
```

```css
// @import "../src/Dropdown.scss";

.demoPadding {
  > button {
    margin: 10px;
  }

  .dropdown-link {
    cursor: pointer;
    margin: 10px;
    font-size: 12px;

    .uf {
      font-size: 12px;
      padding-left: 0px;
    }

    &:hover {
      color: #1890ff;
    }
  }
}
```
