# Approval 审批

审批能力提供审批运行时预加载、审批实例创建、审批面板打开、单据刷新和字段权限转换能力。

## 导入方式

```tsx
import {
  createApprovalRuntimeInstance,
  preloadApprovalRuntime,
  isApprovalRuntimeReady,
  normalizeWorkflowApprovalPermissions,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `preloadApprovalRuntime` | 提前加载审批运行时 |
| `createApprovalRuntimeInstance` | 创建 Web 审批运行时实例 |
| `createApprovalInstance` | 使用自定义 adapter 创建审批实例 |
| `normalizeWorkflowApprovalPermissions` | 将 workflow 字段权限转换为组件权限 patch |
| `resolveApprovalCurrentTaskId` | 从 workflow 字段权限数据中解析当前任务 |

`runtimeResourceBridge`、`isReady`、`preload`、`createInstance` 是运行时桥或别名，通常不作为业务首选表达。

## 最小示例

```tsx
const approval = createApprovalRuntimeInstance({
  app,
  context: {
    billId: record.id,
    businessKey: record.code,
    procinstId: record.procinstId,
    verifyState: record.verifyState,
    initializeInstance: true,
    initializeOptions: {
      appsource: 'ap',
      tenantId,
      busiObj: 'finance.ap.bill',
      billId: record.id,
      formUrls: {
        web: location.href,
        mobile: mobileUrl,
      },
    },
  },
  onRefresh: reloadBill,
  onFieldPermissionsChanged: refreshFieldPermissionState,
});

await approval.ensureReady();
await approval.openPanel();
```

## 关键类型

### ApprovalContext

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `billId` | `string` | 单据 ID |
| `businessKey` | `string` | 审批业务标识 |
| `procinstId` | `string` | 流程实例 ID |
| `verifyState` | `string \| number \| boolean` | 单据审批状态 |
| `initializeInstance` | `boolean` | 是否初始化审批实例 |
| `readyOptions` | `ApprovalRuntimeReadyOptions` | 运行时加载参数 |
| `initializeOptions` | `ApprovalInitializeOptions` | 实例初始化参数 |

### ApprovalInitializeOptions

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `appsource` | `string` | 审批应用来源 |
| `serviceCode` | `string` | 服务编码，默认取 `appsource` |
| `tenantId` | `string` | 租户 ID |
| `busiObj` | `string` | 业务对象编码 |
| `billId` | `string` | 单据 ID |
| `formUrls` | `{ web: string; mobile: string }` | Web 和 Mobile 单据地址 |

### ApprovalInstance

| 方法 | 说明 |
| --- | --- |
| `getSnapshot()` | 获取当前审批实例快照 |
| `ensureReady()` | 加载运行时并初始化实例 |
| `openPanel()` | 打开审批面板 |
| `refresh()` | 执行单据刷新回调 |
| `applyFieldPermissions(patch)` | 增量合并字段权限 |
| `replaceFieldPermissions(patch)` | 替换字段权限 |
| `dispose()` | 销毁审批实例 |

## 常见错误

- `terminalType` 只有 `'1' | '3'`，默认 Web 端是 `'1'`。
- 字段权限不要分散手写转换，优先用 `normalizeWorkflowApprovalPermissions`、`resolveApprovalTaskFieldAuth`。
- 审批动作完成后的单据刷新通过 `onRefresh` 接入，审批实例不应直接读取页面 store。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/approval/docs/README.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/approval/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/approval/src/types.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/approval/src/runtime.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/approval/src/permission.ts`
