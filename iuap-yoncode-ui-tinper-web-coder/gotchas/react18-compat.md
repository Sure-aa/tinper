# React 18 兼容性问题

> 以下问题均在实际项目中验证过，使用者必须了解以避免浪费时间排查。

## React 版本兼容性

**现状**: `peerDependencies` 声明 `"react": "^18.0.0"`，但内部 `wui-core/src/reactCompat.js` 做了 **React 16/18 双版本兼容**，对 `createRoot`、`startTransition`、`flushSync`、`useId` 等均有降级处理。因此实际可运行于 React 16+。
**已知限制**:
- React 19 未经验证，可能存在类型不兼容（`package.json` 声明 `^18.0.0`，不覆盖 19）
- React 16 可以运行，但部分 API（如 `useId`）会降级为 `Math.random()` 实现，可能影响 SSR 场景的 hydration 一致性
**推荐**: React 18.3.1 是最稳妥的版本选择

## forwardRef 控制台警告（全局性，无法消除）

**问题**: 40+ 个组件（Layout、Input、Select、Pagination、Switch、Checkbox、Tooltip、Avatar 等）内部使用 `forwardRef` 但未正确消费第二个参数 `ref`，React 18 会输出警告：
```
forwardRef render functions accept exactly two parameters: props and ref. Did you forget to use the ref parameter?
```
**影响**: 纯控制台噪音，不影响功能。
**方案**: 在入口文件过滤该警告：
```js
const origError = console.error
console.error = (...args) => {
  if (args[0]?.toString?.().includes('forwardRef render functions')) return
  origError.apply(console, args)
}
```

## React.memo + defaultProps 警告（Spin/Loading 组件）

**问题**: `Spin` 的内部 `LoadingComponent` 使用 `React.memo` 包裹 + `defaultProps`，React 18 会输出废弃警告：
```
LoadingComponent: Support for defaultProps will be removed from memo components in a future major release.
```
**影响**: 只要有 `Spin` 或依赖 Spin 的组件（如 Table 的 loading 态），就会触发。不影响功能。
**方案**: 同上，在入口文件过滤。

## StrictMode 放大警告

**问题**: React `StrictMode` 会双重渲染组件，导致上述警告翻倍。
**方案**: 使用 TinperNext 的项目建议去掉 `<StrictMode>` 包裹，改用 `<App />` 直接渲染。

## 推荐的入口文件配置模板

```tsx
import { createRoot } from 'react-dom/client'
import App from './App'

const origWarn = console.warn
const origError = console.error
const suppress = (fn: typeof console.warn) => (...args: any[]) => {
  const msg = args[0]?.toString?.() || ''
  if (msg.includes('forwardRef render functions')) return
  if (msg.includes('defaultProps will be removed')) return
  fn.apply(console, args)
}
console.warn = suppress(origWarn)
console.error = suppress(origError)

createRoot(document.getElementById('root')!).render(<App />)
```
