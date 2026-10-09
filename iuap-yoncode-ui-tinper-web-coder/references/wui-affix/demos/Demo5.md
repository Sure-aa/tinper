---
tags:
  - TinperNext
  - affix组件
---
# 固钉 Affix

## offsetBottom Affix

触发固定的距离屏幕顶部高度等于offetBottom

```tsx
import React, {Component} from 'react';
import {Button, Affix} from '@tinper/next-ui';
class Affix5 extends Component<{}> {
    render() {
	 return (
	   <div className='affixtest'>
                <Affix offsetBottom={20}>
                    <Button colors="primary">20px to affix bottom demo5</Button>
                </Affix>
	   </div>
	 )
    }
}

export default Affix5
```
