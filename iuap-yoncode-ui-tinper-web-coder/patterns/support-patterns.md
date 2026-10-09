# NextPro 支撑服务组合模式

## 列表页 + DataGrid + usePrint

适用：列表行选择后批量打印或预览。

```tsx
const print = usePrint({
  mode: 'list',
  context: printContext,
  records,
  selection: selectedRows,
  getRecordId: row => String(row.id),
});

<Button disabled={!selectedRows.length} onClick={() => print.previewList()}>
  打印预览
</Button>
```

关键点：

- 列表模式必须传 `selection`。
- 选择为空时业务侧应禁用按钮；Hook 内部仍会返回 `NO_SELECTION`。
- 自定义请求封装通过 `apiConfig.request` 或 `api` 接入。

## 卡片页 + DataForm + Draft + Approval

适用：单据新增、编辑、查看页面需要暂存、恢复草稿和发起审批。

```tsx
<DataForm ref={formRef} formMode={formMode}>
  <DataForm.Item name="name" label="名称" inputType="input" required />
</DataForm>

<Button onClick={() => openSaveDraftModal({
  saveDraft,
  updateDraft,
  restoredDraft,
  getPopupContainer,
})}>
  保存草稿
</Button>

<Button onClick={() => approval.openPanel()}>
  审批
</Button>
```

关键点：

- Draft 只调用业务 facade，不定义 payload 结构。
- Approval 通过 `onRefresh` 刷新单据，通过字段权限 API 回写页面权限。
- 微前端场景弹窗要传 `getPopupContainer`。

## 表单字段 + AutoCode

适用：新增态按编码规则自动取号，依赖字段变化时重新判断规则。

```tsx
<AutoCode
  busiObj={busiObj}
  domainKey={domainKey}
  serviceCode={serviceCode}
  field="code"
  mode={formMode}
  value={code}
  source={autoCodeSource}
  onChange={value => formRef.current?.setFieldsValue({ code: value })}
/>
```

关键点：

- `source.getCurrentPageData` 负责读取当前页面数据。
- `source.subscribeDependencies` 负责监听规则依赖字段变化。
- 编辑态不要误触发取号覆盖已有编码。

## 新增页附件 + UploadSession

适用：新增页还没有正式业务 ID，但需要先上传附件，保存后绑定正式对象。

```tsx
const session = useMemo(() => createUploadSession(), []);

<Upload
  value={objectId}
  objectName="billAttachment"
  authId="bill-auth"
  session={session}
  field="attachment"
  mode="add"
  onChange={setObjectId}
/>;

await session.beforeSave();
const saved = await saveBill();
await session.afterSave(slot => saved.attachmentObjectIds[slot.field] || null);
```

关键点：

- 保存前调用 `beforeSave` 检查上传中状态。
- 保存后调用 `afterSave` 绑定正式对象 ID。
- 取消新增或页面卸载时调用 `destroy` 清理临时附件。

## MDF 查询页 + MdfFilter + MdfRefer

适用：MDF 页面需要过滤条件和参照字段共同驱动查询。

```tsx
const filterRef = useRef<MdfFilterPanelRef>(null);

<MdfRefer
  refCode="bd_customer"
  value={customer}
  text={customerName}
  onChange={setCustomer}
  onTextChange={setCustomerName}
/>;

<MdfFilterPanel
  ref={filterRef}
  billNo={billNo}
  domainKey={domainKey}
  serviceCode={serviceCode}
/>;
```

关键点：

- 两者都依赖 MDF runtime，就绪问题先查 `../gotchas/support-gotchas.md`。
- 参照必填校验交给 Form/DataForm，不由 `MdfRefer.required` 完成。
