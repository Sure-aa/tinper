---
tags:
  - TinperNextPro
  - Map组件
---
# Map 地图选点 - 基础示例

## 基本使用

高德地图选点基础用法：默认展示地址回写，配置高德 key 后点击输入框打开地图弹窗，可检索地址、点选位置并回写经纬度。

```tsx
import React from 'react';
import { Map } from 'tne-tinpernextpro-fe';

const Demo1 = () => {
  const [value, setValue] = React.useState<string | undefined>(JSON.stringify({
    address: '北京市朝阳区望京街道',
    longitude: 116.481484,
    latitude: 39.990464,
  }));

  return (
    <div style={{ width: 420 }}>
      <Map
        fieldid="map-demo"
        mapType="amap"
        value={value}
        onChange={setValue}
        placeholder="请输入地址或选择地图位置"
        searchAddress
        // 用你申请的高德 key（可先挂到 window.AMAPKEY / window.AMAPSECRETKEY）
        amapKey={window.AMAPKEY}
        amapSecret={window.AMAPSECRETKEY}
      />
    </div>
  );
};

export default Demo1;
```

### 说明

- `value` 传入 `JSON.stringify(MapValue)` 字符串，`onChange` 受控回写。
- `mapType="amap"` 指定高德；切换百度 / 谷歌只需改 `mapType` 并提供对应 key（`baiduMapKey` / `googleMapKey`）。
- 高德 key 可直接传 prop，也可提前挂到 `window.AMAPKEY` / `window.AMAPSECRETKEY`，组件会自动回退读取。

> 生产环境请使用自己申请的 key，并通过安全密钥和域名白名单做限制。
