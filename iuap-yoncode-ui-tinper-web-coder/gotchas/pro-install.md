# Pro 包安装陷阱

## React 多实例冲突（根本原因与解决方案）

**根本原因**: `tne-tinpernextpro-fe` 的 `package.json` 将 `react` 和 `react-dom` 声明为 **`dependencies`（普通依赖）** 而非 `peerDependencies`（对等依赖）。这导致 npm 安装时会在 `node_modules/tne-tinpernextpro-fe/node_modules/` 下再装一份 React，造成同一页面两个 React 实例，报 `Invalid hook call` 错误。

**Pro 包实际状态**:
- 编译产物（`lib/`）是 Babel 转译，不内联 React（保留 `import from 'react'`）
- `dist/` 产物用 webpack externals 排除了 React（`externals: { react: 'React' }`）
- **问题不在编译产物，而在安装阶段**：npm 按普通依赖装了嵌套 React

**解决方案（按推荐优先级）**:

| 方案 | 配置 | 适用场景 |
| --- | --- | --- |
| **pnpm overrides** | `package.json` 加 `"pnpm": { "overrides": { "react": "18.3.1" } }` | pnpm 项目（推荐） |
| **Vite dedupe** | `vite.config.ts` 加 `resolve: { dedupe: ['react', 'react-dom'] }` | Vite 项目 |
| **Webpack alias** | `resolve.alias { react: path.resolve('./node_modules/react') }` | Webpack 项目 |
| **npm dedupe** | 安装后执行 `npm dedupe` | npm 项目（版本完全一致时生效） |

如果以上方案都无效（极端情况），终极方案是**只用 Base 组件**，不引入 Pro 包。

## 安装必须使用 ynpm

**问题**: TinperNext 不在 npmjs.org 公共仓库维护，`npm install @tinper/next-ui` 会安装到错误的旧版本（如 4.x）或直接 404。

**方案**:
```bash
npm install -g ynpm-tool
ynpm install @tinper/next-ui
```

镜像地址：
- 内网: `https://repo.yyrd.com/artifactory/api/npm/ynpm-all/`
- 外网: `https://repo.yonyoucloud.com/artifactory/api/npm/ynpm-all/`（可能不可达）

## V3R6 包名差异

V3R6 环境包名为 `ynf-tinper-next-pro`，非 V3R6 为 `tne-tinpernextpro-fe`。安装前确认项目环境。
