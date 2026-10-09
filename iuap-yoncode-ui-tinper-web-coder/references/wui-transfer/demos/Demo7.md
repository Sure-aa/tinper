---
tags:
  - TinperNext
  - transfer组件
---
# 穿梭框 Transfer

## 自定义右侧已选列表的排列顺序

`appendToBottom` 参数控制是否将已选项追加到右侧列表末尾，其默认值为false（即将已选项添加到右侧列表最上方）。可在项目中动态改变参数数组targetKeys，穿梭框会根据targetKeys中的顺序进行排序。应用场景：通过上移/下移改变右侧数据顺序。

```tsx
import {Button, Icon, Transfer, TransferProps} from '@tinper/next-ui';
import React from 'react';

interface DemoState {
	targetKeys: TransferProps['selectedKeys'];
	selectedKeys: TransferProps['selectedKeys'];
	showModal: boolean;
	modalSize: string;
}

const allTargetKeys: string[] = [];
const mockData: TransferProps['dataSource'] = [];
for (let i = 0; i < 20; i++) {
    mockData.push({
        key: i.toString(),
        title: `content${i + 1}`,
        description: `description of content${i + 1}`,
    });
    allTargetKeys.push(i.toString());
}

const clsPrefix = 'wui-transfer'

const targetKeys = mockData
    .filter(item => +item.key % 7 === 0)
    .map(item => item.key);

class Demo7 extends React.Component<{}, DemoState> {

	element: React.Component<Partial<TransferProps>> | null = null;

	state: DemoState = {
	    targetKeys,
	    selectedKeys: [],
	    showModal: false,
	    modalSize: ''
	}

	handleChange: TransferProps['onChange'] = (nextTargetKeys, direction, moveKeys) => {
	    this.setState({targetKeys: nextTargetKeys});

	    console.log('targetKeys: ', nextTargetKeys);
	    console.log('direction: ', direction);
	    console.log('moveKeys: ', moveKeys);
	}

	handleSelectChange: TransferProps['onSelectChange'] = (sourceSelectedKeys, targetSelectedKeys) => {
	    this.setState({selectedKeys: [...sourceSelectedKeys, ...targetSelectedKeys]});

	    console.log('sourceSelectedKeys: ', sourceSelectedKeys);
	    console.log('targetSelectedKeys: ', targetSelectedKeys);
	}

	moveAllToRight = () => {
	    this.setState({
	        targetKeys: allTargetKeys
	    })
	}
	moveAllToLeft = () => {
	    this.setState({
	        targetKeys: []
	    })
	}

	swapItems(arr: DemoState['targetKeys'] = [], index1: number, index2: number) {
	    arr[index1] = arr.splice(index2, 1, arr[index1])[0];
	    return arr;
	}

	scopeupRecord(arr: DemoState['targetKeys'], $index: number) {
	    if ($index == 0) {
	        return;
	    }
	    this.swapItems(arr, $index, $index - 1);
	}

	scopedownRecord(arr: DemoState['targetKeys'] = [], $index: number) {
	    if ($index == arr.length - 1) {
	        return;
	    }
	    this.swapItems(arr, $index, $index + 1);
	}

	moveUp = () => {
	    let {targetKeys = [], selectedKeys = []} = this.state
	    let selectedTargetKeys: {key: string, index: number}[] = []
	    targetKeys.forEach((v, i) => {
	        selectedKeys.forEach((v2) => {
	            if (v2 == v) {
	                selectedTargetKeys.push({key: v as string, index: i})
	            }
	        })
	    })
	    if (selectedTargetKeys.length == 1) {
	        this.scopeupRecord(targetKeys, selectedTargetKeys[0].index)
	        this.setState({
	            targetKeys
	        });
	    }
	}

	moveDown = () => {
	    let {targetKeys = [], selectedKeys = []} = this.state
	    let selectedTargetKeys: {key: string, index: number}[] = []
	    targetKeys.forEach((v, i) => {
	        selectedKeys.forEach((v2) => {
	            if (v2 == v) {
	                selectedTargetKeys.push({key: v as string, index: i})
	            }
	        })
	    })
	    console.log(targetKeys, selectedKeys, selectedTargetKeys)
	    if (selectedTargetKeys.length == 1) {
	        this.scopedownRecord(targetKeys, selectedTargetKeys[0].index)
	        this.setState({
	            targetKeys
	        }, () => {
	            const scrollDiv = document.querySelectorAll(`.transfer-demo7 .${clsPrefix}-list-content`)[1]
	            if (scrollDiv) {
	                const index = (selectedTargetKeys[0].index) + 1
	                if (index > 3) {
	                    scrollDiv.scrollTop = (index - 4) * 32;
	                }
	            }
	        });
	    }
	}

	render() {
	    const state = this.state;
	    const { targetKeys } = this.state;
	    return (
	        <div className="transfer-demo7">
	            <Button onClick={this.moveUp} size="lg" className="moveUpBtn moveBtn"><Icon
	                type="uf-arrow-up"/></Button>
	            <Button onClick={this.moveDown} size="lg" className="moveDownBtn moveBtn"><Icon
	                type="uf-arrow-down"/></Button>
	            <Transfer
	                appendToBottom={true}
	                dataSource={mockData}
	                titles={['Source', 'Target']}
	                targetKeys={targetKeys}
	                selectedKeys={state.selectedKeys}
	                onChange={this.handleChange}
	                onSelectChange={this.handleSelectChange}
	                render={item => item.title as string}
	            />
	        </div>
	    );
	}
}


export default Demo7
```

```css
.transfer-demo7 {
  width: 520px;
  position: relative;

  .moveBtn {
    position: absolute;
    right: 0;
    margin: 8px;
    min-width: 40px;
    z-index: 10;
    color: #86939E;
    cursor: pointer;

    &.moveUpBtn {
      margin-top: 62px;
    }

    &.moveDownBtn {
      margin-top: 100px;
    }
  }
}
```
