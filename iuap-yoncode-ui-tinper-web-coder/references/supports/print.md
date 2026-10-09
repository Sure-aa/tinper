# Print 打印

打印能力通过 `usePrint` 提供打印预览、直接打印、打印次数校验、模板选择和打印参数缓存。业务页面决定把打印方法绑定到按钮、菜单、表格操作列或快捷入口。

## 导入方式

```tsx
import {
  PrintProvider,
  buildPluginProtocolUrl,
  buildPrintJob,
  buildPrintParamPayload,
  buildPreviewUrl,
  createHttpPrintApiClient,
  resolvePrintableIds,
  usePrint,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `usePrint` | 打印 Hook，返回预览和打印方法 |
| `PrintProvider` | 设置共享 api、apiConfig、openPreview、下载地址和文案 |
| `createHttpPrintApiClient` | 创建默认 HTTP 打印 API client |
| `buildPrintJob` | 记录转打印任务 |
| `buildPrintParamPayload` | 构建默认打印参数 |
| `buildPreviewUrl` | 构建 Web 打印预览地址 |
| `resolvePrintableIds` | 根据打印次数校验结果解析可打印和跳过单据 |
| `buildPluginProtocolUrl` | 构建本地打印助手兜底协议 |

`TemplateSelectDialog`、`PrintCountDialog`、`PluginWarningDialog` 是内部对话框，业务侧通常通过 `usePrint` 触发。

## 最小示例

```tsx
const print = usePrint({
  mode: 'list',
  context: {
    tenantId,
    locale: 'zh_CN',
    domainKey: 'finance',
    appCode: 'ap',
    billNo: 'AP01',
  },
  records,
  selection,
  getRecordId: row => String(row.id),
  getOrgId: row => row.orgId,
  getTransTypeCode: row => row.transTypeCode,
});

<Button onClick={() => print.previewList()}>打印预览</Button>
<Button onClick={() => print.printList()}>直接打印</Button>
```

## usePrint 参数

| 参数 | 必填 | 说明 |
| --- | --- | --- |
| `mode` | 是 | `'card' \| 'list'`，卡片或列表场景 |
| `context` | 是 | 打印上下文 |
| `records` | 卡片必填，列表可选 | 当前页面记录 |
| `selection` | 列表必填 | 列表模式选中记录 |
| `getRecordId` | 是 | 返回单据 id |
| `getOrgId` | 否 | 返回组织 id |
| `getTransTypeCode` | 否 | 返回交易类型编码 |
| `printCode` | 否 | 指定打印模板编码 |
| `classifyCode` | 否 | 指定模板分类编码 |
| `buildPrintParams` | 否 | 补充业务打印参数 |
| `businessGuard` | 否 | 业务前置校验 |
| `api` / `apiConfig` | 否 | 自定义打印 API client 或默认 HTTP 配置 |
| `openPreview` | 否 | 自定义预览打开方式 |
| `downloadAssistantUrl` | 否 | 打印助手下载地址 |

## 返回值

| 字段 | 说明 |
| --- | --- |
| `state` | 当前打印状态 |
| `execute(action, overrides?)` | 执行指定打印动作 |
| `previewCard()` | 卡片预览 |
| `printCard()` | 卡片直接打印 |
| `previewList()` | 列表预览 |
| `printList()` | 列表直接打印 |

## PrintContext

| 字段 | 必填 | 说明 |
| --- | --- | --- |
| `tenantId` | 是 | 租户 id |
| `locale` | 是 | 语种 |
| `domainKey` | 是 | 领域标识 |
| `appCode` | 是 | 应用编码 |
| `billNo` | 是 | 单据编码 |
| `userId` | 否 | 用户 id |
| `busiObj` | 否 | 业务对象编码 |

## 常见错误

- 列表模式必须传 `selection`，未选择时会进入 `NO_SELECTION` 错误。
- 卡片模式默认使用 `records` 第一条，不要传空数组。
- 直接打印依赖本地打印助手；失败时通过 `buildPluginProtocolUrl` 或下载地址兜底。
- 项目有自定义请求封装时，用 `apiConfig.request` 或自定义 `api` 对接，不要改 Hook 内部逻辑。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/print/docs/README.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/print/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/print/src/types.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/print/src/usePrint.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/print/src/runtime/buildPrintJob.ts`
