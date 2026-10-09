# NextPro 支撑服务常见坑

## Draft

- Draft 不管理业务 payload；保存、更新、列表、恢复、删除都由业务 facade 方法实现。
- `saveInServer` 只透传给 facade，UI 不决定本地或服务端存储。
- 草稿列表必须提供唯一 `id`；`key` 未传时才回退到 `id`。
- 恢复草稿会覆盖当前页面内容，默认确认框可用 `restoreConfirm` 替换。

## Print

- 列表模式 `mode="list"` 必须传 `selection`，卡片模式默认使用 `records[0]`。
- 直接打印依赖本地打印助手；插件调用失败时才走协议兜底或下载提示。
- 打印参数应通过 `buildPrintParams` 在默认参数上补充，不要整段复制旧打印协议后遗漏 `ids`、`billno` 等必需字段。
- 项目请求封装通过 `apiConfig.request` 或自定义 `api` 接入。

## Approval

- 审批字段权限优先用 `normalizeWorkflowApprovalPermissions` 等权限 API 转换，不要分散手写字段映射。
- `ApprovalContext.initializeInstance` 只表示是否初始化实例，运行时加载仍要通过 `ensureReady` 或预加载完成。
- 审批动作后的单据刷新接 `onRefresh`，不要让审批实例直接操作页面 store。

## AutoCode

- `source` 是必填协议，负责读取页面数据和订阅依赖字段；不要只传当前 value。
- 编辑态和浏览态不要自动取号覆盖已有编码。
- 依赖字段变化要通过 `subscribeDependencies` 通知组件刷新规则。

## MDF Refer / Filter

- MDF 参照和过滤都依赖 `window.cb` / MDF runtime；运行时未就绪时先用 `preloadMdfReferRuntime`、`preloadMdfFilterRuntime` 或 Hook 的 `waitReady`。
- `useRefer({ passive: true })`、`useFilter({ passive: true })` 只监听状态，不主动加载 runtime。
- `MdfRefer.required` 是兼容字段，不执行表单必填校验。
- `MdfFilterPanel.getConditions()` 需要 runtime 已就绪并完成渲染。

## Upload

- 新增页没有正式对象 ID 时，用 `createUploadSession` 管理临时附件，保存后 `afterSave` 绑定正式 ID。
- 保存前调用 `beforeSave`，否则可能在文件仍上传中时提交业务单据。
- `objectName`、`authId` 是文件服务关键参数，不能用前端字段名随意代替。
- trigger 模式数量展示默认会查询附件数量；不需要时设 `countStrategy="none"`。

## 微前端浮层

涉及 Modal、Notification、上传弹窗、MDF 浮层等能力时，继续遵守核心规则中的 `getPopupContainer` 要求，避免浮层挂到 `document.body` 导致沙箱逃逸。
