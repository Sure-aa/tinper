# NextPro 支撑服务路由

支撑服务不是普通 UI 组件。遇到审批、草稿、打印、上传、自动编码、MDF 参照、MDF 过滤等需求时，先按本表定位，再读对应 reference。

| 用户需求关键词 | 优先查看 | 推荐入口 |
| --- | --- | --- |
| 审批、审批流、流程实例、审批面板、字段权限 | `../references/supports/approval.md` | `createApprovalRuntimeInstance` |
| 自动编码、编码规则、单据编号、取号 | `../references/supports/autoCode.md` | `AutoCode` / `useAutoCode` |
| 保存草稿、草稿管理、恢复草稿、暂存 | `../references/supports/draft.md` | `openSaveDraftModal` / `openDraftManager` |
| MDF 过滤、查询过滤条件、过滤面板 | `../references/supports/mdfFilter.md` | `MdfFilterPanel` / `useFilter` |
| MDF 参照、参照选择、范围过滤、ReferModel | `../references/supports/mdfRefer.md` | `MdfRefer` / `useRefer` |
| 打印、打印预览、直接打印、打印助手、打印次数 | `../references/supports/print.md` | `usePrint` |
| 上传、附件、文件服务、临时附件、附件数量 | `../references/supports/upload.md` | `Upload` / `createUploadSession` |

## 选型提示

- 打印优先 `usePrint`，业务侧把 `previewList`、`printList`、`previewCard`、`printCard` 绑定到按钮或操作列。
- 草稿优先命令式 `openSaveDraftModal` / `openDraftManager`；需要统一弹窗状态时再用声明式组件。
- 上传新增页优先配合 `createUploadSession` 管理临时附件和保存后绑定。
