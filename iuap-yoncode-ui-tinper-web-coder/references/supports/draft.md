# Draft 草稿

草稿能力提供保存草稿、草稿管理、草稿列表展示和恢复确认能力。业务页面负责实现保存、更新、列表、恢复、删除等 facade 方法；Draft 组件只负责弹窗 UI、确认操作和调用 facade。

## 导入方式

```tsx
import {
  DraftList,
  DraftManagerModal,
  DraftSaveModal,
  openDraftManager,
  openSaveDraftModal,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `openSaveDraftModal` | 命令式打开保存草稿弹窗 |
| `openDraftManager` | 命令式打开草稿管理弹窗 |
| `DraftSaveModal` | 声明式保存草稿弹窗 |
| `DraftManagerModal` | 声明式草稿管理弹窗 |
| `DraftList` | 自定义弹窗外壳时直接渲染草稿列表 |

## 最小示例

```tsx
openSaveDraftModal({
  saveDraft: controller.saveDraft,
  updateDraft: controller.updateDraft,
  restoredDraft: controller.restoredDraft,
  getPopupContainer,
  onSaved: () => Message.success('保存成功'),
  onError: error => Message.error(String(error)),
});

openDraftManager({
  listDrafts: controller.listDrafts,
  restoreDraft: controller.restoreDraft,
  deleteDraft: controller.deleteDraft,
  closeAfterRestore: true,
  getPopupContainer,
});
```

## Facade 方法

```ts
type SaveDraftMethod = (input: DraftSaveManualInput) => Promise<DraftSaveResult>;
type UpdateDraftMethod = (input: DraftUpdateManualInput) => Promise<DraftSaveResult>;
type RestoredDraftMethod = () => DraftRestoredSource | null | undefined;
type ListDraftsMethod = (input?: DraftListManualInput) => Promise<DraftSummary[]>;
type RestoreDraftMethod = (input: DraftRestoreManualInput) => Promise<DraftRestoreResult>;
type DeleteDraftMethod = (input: DraftDeleteManualInput) => Promise<void>;
```

## 关键参数

| 参数 | 适用入口 | 说明 |
| --- | --- | --- |
| `saveDraft` | 保存弹窗 | 保存为新草稿，必填 |
| `updateDraft` | 保存弹窗 | 更新已恢复草稿 |
| `restoredDraft` | 保存弹窗 | 返回当前页面恢复来源 |
| `listDrafts` | 管理弹窗 | 查询草稿列表，必填 |
| `restoreDraft` | 管理弹窗 | 恢复指定草稿，必填 |
| `deleteDraft` | 管理弹窗 | 删除指定草稿，必填 |
| `saveInServer` | 两类弹窗 | 只透传给 facade，UI 不决定存储位置 |
| `getPopupContainer` | 两类弹窗 | 微前端浮层挂载容器 |
| `container` | 命令式弹窗 | 命令式弹窗 root 容器，默认 `document.body` |

## DraftSummary 字段

草稿列表必须提供唯一 `id`。`key` 未传时使用 `id`。

| 字段 | 说明 |
| --- | --- |
| `id` | 草稿唯一标识，必填 |
| `title` / `name` | 草稿名称 |
| `updatedAt` / `updateTime` / `createdAt` | 时间展示 |
| `updaterName` / `updatedByName` / `creatorName` / `createdByName` | 人员展示 |

## 常见错误

- Draft UI 不接收完整 controller，也不直接读取业务运行时状态。
- 表单数据、草稿 payload、服务端接口、恢复后的页面回写都由业务侧控制。
- 恢复草稿会覆盖当前页面内容，默认弹确认框；可用 `restoreConfirm` 自定义。
- 从已恢复草稿再次保存时，只有同时提供 `restoredDraft` 和 `updateDraft` 才显示“更新原草稿”和“保存新草稿”。
- 微前端场景建议传 `getPopupContainer`。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/draft/docs/README.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/draft/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/draft/src/types.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/draft/src/openSaveDraftModal.tsx`
- `node_modules/tne-tinpernextpro-fe/src/supports/draft/src/openDraftManager.tsx`
