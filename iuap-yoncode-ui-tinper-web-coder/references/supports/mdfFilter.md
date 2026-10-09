# MdfFilter MDF 过滤

MDF 过滤能力用于加载 MDF 运行时，在指定 DOM 中渲染过滤面板，并读取当前过滤条件。

## 导入方式

```tsx
import {
  MdfFilterPanel,
  useFilter,
  preloadMdfFilterRuntime,
  isMdfFilterRuntimeReady,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `MdfFilterPanel` | 直接渲染 MDF 过滤面板 |
| `useFilter` | 自定义加载流程时监听或等待 MDF 运行时 |
| `preloadMdfFilterRuntime` | 提前加载 MDF 过滤运行时 |
| `mdfFilterRuntimeResourceBridge` | Runtime Bridge 场景使用 |

## 最小示例

```tsx
const filterRef = useRef<MdfFilterPanelRef>(null);

<MdfFilterPanel
  ref={filterRef}
  billNo="F22899_orderRecheckList"
  domainKey="c-ord-recheck-test"
  serviceCode="orderRecheck"
  query={{ pageCode: 'list' }}
  onReady={() => filterRef.current?.rerender()}
  onError={error => Message.error(String(error))}
/>;

const conditions = await filterRef.current?.getConditions();
```

## 关键 Props

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `billNo` | `string` | 单据编码，必填 |
| `domainKey` | `string` | 领域标识，必填 |
| `serviceCode` | `string` | 服务编码，必填 |
| `query` | `Record<string, any>` | 查询扩展参数 |
| `condition` | `Record<string, any>` | 初始条件 |
| `isMobile` | `boolean` | 是否移动端 |
| `visible` | `boolean` | 是否渲染 |
| `timeoutMs` | `number` | 等待 MDF 运行时超时时间 |
| `onReady` | `() => void` | 运行时就绪回调 |
| `onError` | `(error: unknown) => void` | 加载或渲染错误 |

## Ref 方法

| 方法 | 说明 |
| --- | --- |
| `getConditions()` | 读取当前过滤条件 |
| `rerender()` | 重新渲染过滤面板 |

## useFilter

```ts
const { ready, cb, waitReady } = useFilter({
  timeoutMs: 10000,
  passive: false,
});
```

`ready` 表示 MDF 运行时是否就绪；`cb` 是就绪后的 `window.cb`；`waitReady` 可主动等待运行时。

## 常见错误

- MDF 过滤依赖 MDF runtime，渲染前要等待 `cb.cn.filter.render` 可用。
- `getConditions` 依赖 `billNo`、`domainKey` 和 `isMobile`，不要只传前端表单字段。
- `passive: true` 只监听状态，不主动预加载。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/mdfFilter/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfFilter/src/iMdfFilter.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfFilter/src/MdfFilterPanel.tsx`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfFilter/src/useFilter.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/mdfFilter/src/MdfFilterEnv.ts`
