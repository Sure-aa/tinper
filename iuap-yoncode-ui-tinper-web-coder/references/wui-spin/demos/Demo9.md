---
tags:
  - TinperNext
  - spin组件
---
# 加载提示 Spin

## loadingType为cricle

```tsx
import {Spin, Pagination} from '@tinper/next-ui';
import React, {useState} from 'react';

const App: React.FC = () => {
    const [activePage, setActivePage] = useState<number>(1);

    const handleSelect = (activePage: number) => {
        setActivePage(activePage)
    };
    const onPageSizeChange = (activePage: number, _pageSize: number) => {
        setActivePage(activePage)
    };
    return (
        <div>
            <Spin loadingType='cricle' spinning getPopupContainer={() => document.getElementById('demo9-pagination')} />
            <Pagination id="demo9-pagination" style={{display: 'inline-flex', position: 'relative'}} showSizeChanger pageSizeOptions={["10", "20", "30", "50", "80"]} total={300} defaultPageSize={20} current={activePage} onChange={handleSelect} onPageSizeChange={onPageSizeChange}/>
        </div>
    )
}


export default App;
```
