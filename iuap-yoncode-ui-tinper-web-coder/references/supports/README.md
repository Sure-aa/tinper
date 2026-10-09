# NextPro 支撑服务总览

支撑服务是 `tne-tinpernextpro-fe/src/supports` 导出的业务能力，不是普通展示组件。遇到审批、自动编码、草稿、MDF 参照、MDF 过滤、打印、上传等需求时，先查本目录。

## 导入方式

```tsx
import {
  Upload,
  usePrint,
  openDraftManager,
} from 'tne-tinpernextpro-fe/supports';
```

部分能力也可能从包根或独立入口导出。以各能力 reference 中的导入示例为准。

## 能力索引

| 能力 | 模块 | 推荐入口 | 典型场景 | 文档 |
| --- | --- | --- | --- | --- |
| 审批 | approval | `createApprovalRuntimeInstance` | 单据审批、审批面板、字段权限 | `./approval.md` |
| 自动编码 | autoCode | `AutoCode` / `useAutoCode` | 编码规则、单据编号自动生成 | `./autoCode.md` |
| 草稿 | draft | `openSaveDraftModal` / `openDraftManager` | 保存草稿、草稿管理、恢复草稿 | `./draft.md` |
| MDF 过滤 | mdfFilter | `MdfFilterPanel` / `useFilter` | MDF 查询过滤条件渲染和读取 | `./mdfFilter.md` |
| MDF 参照 | mdfRefer | `MdfRefer` / `useRefer` | MDF 参照选择、范围过滤 | `./mdfRefer.md` |
| 打印 | print | `usePrint` | 打印预览、直接打印、打印次数校验 | `./print.md` |
| 上传 | upload | `Upload` / `createUploadSession` | 文件上传、附件数量、保存前后绑定 | `./upload.md` |

## 使用边界

- 支撑服务需要业务侧显式传入上下文、request/transport、facade 方法或 runtime adapter，不要假设全局 store 存在。
- 业务侧优先使用 reference 标为“推荐入口”的 API；内部 workbench、dialog、table、progress 组件只在文档明确说明时直接使用。
- 文档缺失或矛盾时查源码：`node_modules/tne-tinpernextpro-fe/src/supports/<module>/src`。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/*/docs`
- `node_modules/tne-tinpernextpro-fe/src/supports/*/src/index.ts`
