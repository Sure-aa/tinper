---
tags:
  - TinperNextPro
  - Map组件
---

# Map 地图选点

<!--Map-->
`Map` 是 TinperNextPro 提供的地图选点 / 地址录入组件，统一封装了**高德地图（amap）、百度地图（baidu）、谷歌地图（google）** 三种服务商，对外暴露一致的 API。支持地址检索、地图选点、经纬度回写、浏览态展示，以及多边形 / 圆形 / 线路 / 导航路径等区域绘制能力。

> 该组件已从原低代码平台迁入 `tne-tinpernextpro-fe`，移除了低代码运行时依赖，保留 Web 端地图检索、选点、浏览态及多服务商能力。

## ⚠️ 前置准备：必须配置地图 key

地图资源由第三方服务商提供，**使用前必须申请并配置对应服务商的 key**，否则组件只会显示「未配置」提示，不会加载地图。

- 高德：`amapKey` + `amapSecret`（安全密钥）
- 百度：`baiduMapKey` + `baiduMapSecret`
- 谷歌：`googleMapKey`

key 来源优先级：**显式传入的 prop > `window` 全局变量**（`window.AMAPKEY` / `window.AMAPSECRETKEY` / `window.BMAPKEY` / `window.BMAPSECRETKEY`）。

> 请使用你自己申请的 key。示例中的 key 仅为演示占位，不要直接用于生产。

## 快速使用

```tsx
import React, { useState } from 'react';
import { Map } from 'tne-tinpernextpro-fe';
import type { MapValue } from 'tne-tinpernextpro-fe';

export default function MapDemo() {
  // value 推荐传 JSON.stringify(MapValue) 后的字符串
  const [value, setValue] = useState<string | undefined>(JSON.stringify({
    address: '北京市朝阳区望京街道',
    longitude: 116.481488,
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
        searchAddress                 // 允许地址搜索（默认 true）
        amapKey={window.AMAPKEY}      // 用你申请的高德 key
        amapSecret={window.AMAPSECRETKEY}
      />
    </div>
  );
}
```

输入框聚焦后打开地图弹窗，可检索地址、点选位置；确认后通过 `onChange` 回写序列化字符串。

## value / onChange 约定

- `value`：推荐传入 `JSON.stringify(MapValue)` 的**字符串**（也接受 `MapValue` 对象）。
- `onChange(value?: string)`：值变化时回调，返回**序列化后的字符串**。需外部受控 `setState` 才能回写。

```ts
interface MapValue {
  longitude?: number;   // 经度
  latitude?: number;    // 纬度
  address?: string;     // 详细地址
  province?: string;    // 省
  city?: string;        // 市
  district?: string;    // 区
  adcode?: string;      // 行政区划代码
  country?: string;     // 国家
  areaData?: {          // 区域绘制结果
    type?: 'polygon' | 'line' | 'point';
    path?: Array<{ longitude: number; latitude: number }>;
  };
}
```

`MapValue` 还包含 `name`、`place_id`、`uid`、`location`、`searchAddress` 等服务商返回的附加字段，按需取用。

## 三种地图服务商

| `mapType` | 服务商 | 必需 key | 全局回退 |
|-----------|--------|----------|----------|
| `'amap'` | 高德地图 | `amapKey` + `amapSecret` | `window.AMAPKEY` / `window.AMAPSECRETKEY` |
| `'baidu'` | 百度地图 | `baiduMapKey` + `baiduMapSecret` | `window.BMAPKEY` / `window.BMAPSECRETKEY` |
| `'google'` | Google Maps | `googleMapKey` | — |

未显式传 `mapType` 时组件会自动判断。未配置对应 key 时，组件展示未配置提示，不发起资源加载。

## API

### 基础（CommonMapProps）

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `MapValue \| string` | — | 地图值，推荐 `JSON.stringify(MapValue)` 字符串 |
| `onChange` | `(value?: string) => void` | — | 值变化回调，返回序列化字符串 |
| `mapType` | `'amap' \| 'baidu' \| 'google'` | 自动判断 | 地图服务商 |
| `amapKey` / `amapSecret` | `string` | `window.AMAPKEY` 等 | 高德 key / 安全密钥 |
| `baiduMapKey` / `baiduMapSecret` | `string` | `window.BMAPKEY` 等 | 百度 key / 密钥 |
| `googleMapKey` | `string` | — | Google Maps key |
| `showType` | `'address' \| 'location'` | `'address'` | 输入框展示地址或经纬度 |
| `searchAddress` | `boolean` | `true` | 是否允许地址搜索 |
| `markDrag` | `boolean` | — | 是否允许拖拽标记点 |
| `mapIsCanModify` | `boolean` | `true` | 是否允许手动修改 |
| `isContainModal` | `boolean` | `true` | 是否通过弹窗展示地图 |
| `placeholder` | `string` | 语言包默认值 | 输入占位文案 |
| `disabled` | `boolean` | `false` | 禁用 |
| `readOnly` / `isReadOnly` | `boolean` | `false` | 只读 |
| `size` | `'xs'\|'sm'\|'md'\|'nm'\|'lg'\|...` | — | 尺寸 |
| `bordered` | `boolean \| 'bottom' \| 0\|1\|2` | `true` | 边框模式 |
| `locale` | `string` | — | 国际化语言 |
| `fieldid` | `string` | — | 字段标识（无障碍/测试） |
| `commonOption` | `Record<string, any>` | — | 透传给底层地图的通用配置 |

### 浏览态

| 参数 | 类型 | 说明 |
|------|------|------|
| `browser` | `boolean` | 是否浏览态（默认 `false`） |
| `browserValueRender` | `(value?: MapValue) => ReactNode` | 浏览态自定义渲染 |
| `noDataText` | `string` | 浏览态空值展示（默认 `--`） |
| `browserStyle` / `browserClassName` | — | 浏览态样式 / 类名 |

```tsx
// 浏览态只读展示
<Map value={value} browser browserValueRender={v => v?.address || '--'} />
```

### 高级：区域绘制 / 导航（AdvancedMapProps）

除选点外，组件还支持在地图上绘制并回写区域数据，能力由各服务商 SDK 提供，需配合对应 key 使用：

| 参数 | 类型 | 说明 |
|------|------|------|
| `mapConfig` | `Record<string, any>` | 底层地图初始化配置 |
| `zoom` | `number` | 缩放级别 |
| `areaType` | `'polygon' \| 'line' \| 'point'` | 区域类型 |
| `areaPath` / `polygonPath` | `MapAreaPoint[]` | 多边形 / 区域路径坐标 |
| `circleRadius` | `number` | 圆形半径 |
| `polygonStyle` / `polylineStyle` | `Record<string, any>` | 多边形 / 线样式 |
| `deliveryMethod` | `'polygon' \| 'circle' \| 'multiplepolygon' \| 'navigate'` | 配送 / 绘制方式（`navigate` 为导航路径） |
| `deliveryMethodOptions` | `DeliveryMethod[]` | 可选的绘制方式 |
| `searchRegion` | `string` | 搜索区域限制 |
| `openService` | `string` | 开启的服务 |
| `bubble` | `boolean` | 气泡 |
| `onAmapHandleClick` | `(e) => boolean \| void` | 地图点击（高德） |
| `onChangePolygonPath` | `(path) => void` | 多边形路径变化 |
| `onChangeCircleRadius` | `(radius: number) => void` | 圆形半径变化 |
| `onChangeNavigateRes` | `(res) => void` | 导航结果变化 |
| `colNumber` | `number` | 列数（多组件排列） |
| `smallStyles` / `modalStyles` / `bigStyles` | `CSSProperties` | 小图 / 弹窗 / 大图样式 |

```ts
interface MapAreaPoint {
  longitude: number;
  latitude: number;
  lng?: number;
  lat?: number;
}
```

> 区域绘制 / 导航属于高级能力，依赖对应服务商 SDK 的具体能力，使用前请确认目标 `mapType` 支持。

## 易踩坑

- **未配置 key 不报错但不显示地图**：组件会展示「未配置」提示。先确认 `mapType` 对应的 key 已通过 prop 或 `window` 全局变量提供。
- **value 不回写**：`onChange` 返回的是字符串，外部必须受控 `setState`，否则输入框不会更新。
- **`onChange` 拿不到对象**：回调返回的是**序列化字符串**，需要 `JSON.parse` 才能得到 `MapValue`。
- **`mapIsCanModify` / `markDrag`**：默认允许修改；设为 `false` 时地图仅用于展示，无法选点。
- **`isContainModal`**：默认走弹窗选点；若需要内联展示地图，需调整该配置并自行处理布局尺寸。
- **key 安全**：前端 key 仍会暴露在浏览器，请使用服务商提供的安全密钥（如高德 `amapSecret`）和域名白名单限制，不要把敏感业务凭证放进来。

## 相关

- 安装与包名见 `../README.md`。
- 其它输入组件（Email / Phone / Mobile / Identity / InputMultilang）见各自 `readme.md`。
