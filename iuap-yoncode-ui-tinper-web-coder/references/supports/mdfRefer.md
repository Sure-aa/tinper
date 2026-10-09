# MdfRefer MDF 参照

MDF 参照能力用于在 React 页面中接入 MDF ReferModel，支持普通参照、列表参照、树参照、多选、浏览态、范围过滤和 runtime 预加载。

## 导入方式

```tsx
import {
  MdfRefer,
  useRefer,
  preloadMdfReferRuntime,
  bindRangeParamsToReferModel,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `MdfRefer` | 直接渲染 MDF 参照控件 |
| `useRefer` | 自定义加载流程时监听或等待 MDF 运行时 |
| `preloadMdfReferRuntime` | 提前加载 MDF 参照运行时 |
| `bindRangeParamsToReferModel` | 给参照列表或树请求绑定范围参数 |

## 最小示例

```tsx
<MdfRefer
  refCode="bd_customer"
  domainKey="c-ord-recheck-test"
  serviceCode="orderRecheck"
  busiObj="orderRecheck.orderRecheck.F22899_orderRecheck"
  billNum="F22899_orderRecheck"
  value={customer}
  text={customerName}
  multiple={false}
  onChange={value => setCustomer(value)}
  onTextChange={text => setCustomerName(text)}
/>
```

## 关键 Props

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `refCode` | `string` | MDF 参照编码，必填 |
| `displayName` | `string` | 参照对象显示字段，默认 `name` |
| `valueField` | `string` | 参照对象值字段，默认 `id` |
| `domainKey` | `string` | 领域标识 |
| `serviceCode` | `string` | 服务编码，未传时使用 `busiObj` |
| `busiObj` | `string` | 业务对象编码 |
| `billNum` | `string` | 单据编码 |
| `multiple` | `boolean` | 是否多选 |
| `value` / `text` | `any` / `string` | 当前值和显示文本 |
| `modelName` | `'refer' \| 'listrefer' \| 'treerefer'` | MDF 参照模型类型 |
| `lazyLoad` | `boolean` | 是否首次点击或聚焦时加载 runtime，默认 `true` |
| `relevantRange` | `MdfReferRangeParams` | MDF 范围过滤参数 |

## Ref 方法

| 方法 | 说明 |
| --- | --- |
| `getValue()` | 获取 ReferModel 当前值 |
| `setValue(value)` | 设置 ReferModel 当前值 |
| `setEnable(enabled)` | 设置是否可编辑 |

## useRefer

```ts
const { ready, cb, waitReady } = useRefer({
  timeoutMs: 10000,
  passive: false,
});
```

`ready` 表示 MDF 运行时是否就绪；`cb` 是就绪后的 `window.cb`；`waitReady` 可主动等待运行时。

## 常见错误

- `required` 是兼容字段，组件自身不执行必填校验；表单校验仍应由 `Form/DataForm` 管理。
- `lazyLoad` 默认为 `true`，需要首屏提前加载时主动调用 `preloadMdfReferRuntime`。
- 清空时 `onChange` 返回 `null`，`onTextChange` 返回空字符串。
- 范围过滤使用 `relevantRange`，不要在 `config` 中手写和后端协议不一致的参数。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/mdfRefer/docs/README.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfRefer/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfRefer/src/iMdfRefer.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfRefer/src/MdfRefer.tsx`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfRefer/src/rangeParams.ts`
