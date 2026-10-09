# Upload 上传

上传能力提供文件上传 UI、附件数量刷新、临时附件保存前检查、保存后绑定正式对象 ID 和资源预加载能力。

## 导入方式

```tsx
import {
  Upload,
  createUploadSession,
  createAttachmentSession,
  preloadUploadResources,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `Upload` | 文件上传或附件入口组件 |
| `createUploadSession` | 页面级上传会话，协调多个附件位 |
| `createAttachmentSession` | `createUploadSession` 的附件语义别名 |
| `preloadUploadResources` | 提前加载文件 SDK 或资源 |

## 最小示例

```tsx
const session = useMemo(() => createUploadSession(), []);

<Upload
  value={objectId}
  objectName="orderAttachment"
  authId="order-recheck"
  session={session}
  field="attachment"
  mode={pageMode}
  displayMode="trigger"
  triggerText="附件"
  onChange={nextObjectId => setObjectId(nextObjectId)}
  onError={error => Message.error(error.message)}
/>;

await session.beforeSave();
await saveBill();
await session.afterSave(slot => savedObjectIds[slot.field] || null);
```

## 关键 Props

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `value` | `string \| null` | 当前附件对象 ID |
| `objectName` | `string` | 附件所属对象名，必填 |
| `authId` | `string` | 文件服务鉴权标识，必填 |
| `session` | `UploadSession` | 页面级附件会话 |
| `field` / `storeId` / `rowId` | `string` | 接入 session 时标识附件位置 |
| `mode` | `'add' \| 'edit' \| 'browse'` | 页面状态，默认 `browse` |
| `displayMode` | `'panel' \| 'trigger'` | 展示模式，默认 `panel` |
| `countStrategy` | `'query' \| 'none'` | trigger 模式附件数量查询策略 |
| `uploadType` | `'file' \| 'block'` | 文件列表展示类型 |
| `maxCount` / `maxSize` | `number` | 最大文件数量和单文件大小 |
| `beforeUpload` | `(data) => boolean \| Promise<boolean>` | 上传前校验 |
| `onChange` | `(value: string \| null) => void` | 附件对象 ID 变化 |
| `onFileUploadCallBack` | `(file, fileList) => void` | 文件上传成功 |
| `onFileDeleteCallBack` | `(payload) => void` | 文件删除 |

## UploadSession

| 方法 | 说明 |
| --- | --- |
| `register(slot)` | 注册附件位置，返回注销函数 |
| `refreshCounts(input?)` | 批量刷新附件数量 |
| `beforeSave()` | 保存前检查是否存在上传中的附件 |
| `afterSave(resolveObjectId)` | 保存后将临时附件绑定到正式对象 ID |
| `destroy()` | 清理临时附件和会话状态 |

## UploadRef

| 方法 | 说明 |
| --- | --- |
| `getState()` | 获取当前附件状态 |
| `commit(nextObjectId)` | 将临时附件绑定到正式对象 ID |
| `dispose()` | 清理当前实例的临时附件 |

## 常见错误

- 新增页没有正式业务 ID 时，用 session 管理临时附件，保存后再 `afterSave` 绑定正式 ID。
- `displayMode="trigger"` 的附件数量默认按 `countStrategy="query"` 查询；不需要数量时设为 `none`。
- `objectName` 和 `authId` 是文件服务识别附件归属和鉴权的关键字段，不能只传前端字段名。
- 页面卸载或取消新增时要调用 session/ref 的清理方法，避免临时附件残留。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/upload/docs/readme.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/upload/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/upload/src/types.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/upload/src/upload.tsx`
- `node_modules/tne-tinpernextpro-fe/src/supports/upload/src/session.ts`
