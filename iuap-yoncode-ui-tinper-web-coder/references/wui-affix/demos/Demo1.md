---
tags:
  - TinperNext
  - affix组件
---
# 固钉 Affix

## 基本的Affix,带有getPopupContainer

基本的Affix,带有getPopupContainer

```tsx
import {Affix, Button, AffixProps} from '@tinper/next-ui';
import React, {Component} from 'react';

interface AffixState {
	container: HTMLElement | null;
}

class Demo1 extends Component<{}, AffixState> {
    constructor(props: {}) {
        super(props);
        this.state = {
            container: null,
        }
    }

	getTarget = () => {
	    return document.getElementById('out-wrapper')
	}

	targetChange: AffixProps['onTargetChange'] = (val) => {
	    console.log(val)
	}

	change: AffixProps['onChange'] = ({affixed, event}) => {
	    console.log('affixed', affixed)
	    console.log('event', event)
	}

	componentDidMount() {
	    if (document.getElementById('outer-box')) {
	        this.setState({container: document.getElementById('outer-box')})
	    }
	}

	render() {
	    return (
	        <div className="demo1">
	            <div>某个div内的affix，getPopupContainer canHidden=true zIndex=2001</div>
	            <div className="out-wrapper" id="out-wrapper">
	                <div className="outer-box checkered stripes" id="outer-box">
	                    <Affix getPopupContainer={this.state.container} target={this.getTarget} canHidden={true}
							   zIndex={2001} onTargetChange={this.targetChange} onChange={this.change}>
	                        <Button colors="primary">affix in container</Button>
	                    </Affix>
	                </div>
	            </div>
	        </div>
	    )
	}
}


export default Demo1;
```

```css
.demo1 {
  // float: left;
}

.stripes {
  width: 500px;
  height: 400px !important;;
  // float: left;

  margin: 10px;

  -webkit-background-size: 16px 16px;
  -moz-background-size: 16px 16px;
  background-size: 16px 16px; /* 控制条纹的大小 */

  -moz-box-shadow: 1px 1px 8px #ccc;
  -webkit-box-shadow: 1px 1px 8px #ccc;
  box-shadow: 1px 1px 8px #ccc;
}

.out-wrapper {
  height: 100px;
  width: 527px;
  overflow-y: scroll;
}

.checkered {
  padding-top: 40px;
  background-image: -webkit-gradient(linear, 0 0, 100% 100%, color-stop(.25, #ccc), color-stop(.25, transparent), to(transparent)),
  -webkit-gradient(linear, 0 100%, 100% 0, color-stop(.25, #ccc), color-stop(.25, transparent), to(transparent)),
  -webkit-gradient(linear, 0 0, 100% 100%, color-stop(.75, transparent), color-stop(.75, #ccc)),
  -webkit-gradient(linear, 0 100%, 100% 0, color-stop(.75, transparent), color-stop(.75, #ccc));
  background-image: -moz-linear-gradient(45deg, #ccc 25%, transparent 25%, transparent),
  -moz-linear-gradient(-45deg, #ccc 25%, transparent 25%, transparent),
  -moz-linear-gradient(45deg, transparent 75%, #ccc 75%),
  -moz-linear-gradient(-45deg, transparent 75%, #ccc 75%);
  background-image: -o-linear-gradient(45deg, #ccc 25%, transparent 25%, transparent),
  -o-linear-gradient(-45deg, #ccc 25%, transparent 25%, transparent),
  -o-linear-gradient(45deg, transparent 75%, #ccc 75%),
  -o-linear-gradient(-45deg, transparent 75%, #ccc 75%);
  background-image: linear-gradient(45deg, #ccc 25%, transparent 25%, transparent),
  linear-gradient(-45deg, #ccc 25%, transparent 25%, transparent),
  linear-gradient(45deg, transparent 75%, #ccc 75%),
  linear-gradient(-45deg, transparent 75%, #ccc 75%);
}
.affixtest{
  overflow: auto;
  .affixTitle{
    width: 100%;
    height: 30px;
    line-height: 30px;
    background-color: aquamarine;
  }
}
.out-wrapper-f {
  height: 300px;
  background: #ccc;
  //border-bottom: 1px solid #e3e7ee;
  // overflow: scroll;
  overflow-y: scroll;
}
}
.affixF{
.wui-affix-content{
  background: #f7f7f7;
  top: 30px;
}
```
