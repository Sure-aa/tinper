# Form 使用模式（来自真实项目蒸馏）

## 1. Form 三种 API 风格

| 风格 | 适用场景 | 示例 |
|------|---------|------|
| `Form.useForm()` Hook 式 | 函数组件（推荐） | `const [form] = Form.useForm()` |
| `Form.createForm()` HOC 式 | 类组件/旧项目 | `export default Form.createForm()(MyComp)` |
| `ref={formRef}` Ref 式 | DataForm/SearchForm | `formRef.current.validateFields()` |

新项目统一用 Hook 式或 Ref 式，不再推荐 HOC 式。

**validateFields 风格差异**：
- Hook 式 / Ref 式：只支持 Promise（`await form.validateFields()`）
- HOC 式：同时支持回调和 Promise，旧项目多用回调风格 `validateFields((err, values) => {})`
- 迁移时去掉回调参数即可切换为 Promise 风格

## 2. DataForm inputType 优先原则

使用 DataForm 时优先用内置 inputType 声明表单项，不要在 DataForm 内嵌套手写 wui-xxx 组件：

```jsx
// ✅ 正确 — 用 inputType
<DataForm.Item label="部门" name="dept" inputType="select"
  options={[{ label: '技术部', value: '1' }]} />

// ❌ 不推荐 — 在 DataForm 内手写组件
<DataForm.Item label="部门" name="dept" inputType="custom"
  render={() => <Select options={[...]} />} />
```

只有 inputType 22 种枚举覆盖不到时，才用 `inputType="custom"`。

## 3. Form.List 动态字段

配合 add/remove 做可增减的表单行：

```jsx
<Form.List name="contacts">
  {(fields, { add, remove }) => (
    <>
      {fields.map((field) => (
        <Space key={field.key}>
          <Form.Item {...field} name={[field.name, 'name']} rules={[{ required: true }]}>
            <Input placeholder="姓名" />
          </Form.Item>
          <Form.Item {...field} name={[field.name, 'phone']}>
            <Input placeholder="电话" />
          </Form.Item>
          <Button onClick={() => remove(field.name)}>删除</Button>
        </Space>
      ))}
      <Button onClick={() => add()}>添加联系人</Button>
    </>
  )}
</Form.List>
```

## 4. DataForm custom 类型注意事项

`custom` 类型的控件会自动注入 `value`/`onChange`，数据同步由 Form 接管：

```jsx
<DataForm.Item label="自定义" name="custom" inputType="custom"
  render={(props) => (
    <MyCustomInput value={props.value} onChange={props.onChange} />
  )}
/>
```

- 禁止用 `defaultValue` 设置值，应通过 `initialValues` 或 `setFieldsValue`
- 自定义组件必须消费 `value` 和 `onChange`

## 5. SearchForm + DataTable 联动

```jsx
const searchRef = useRef();
const tableRef = useRef();

<SearchForm ref={searchRef} formLayout={4} collapsedNumber={1}
  onSearch={(values) => {
    tableRef.current?.reload();
  }}
  onReset={() => {
    tableRef.current?.reload();
  }}>
  <SearchForm.Item label="名称" name="name" inputType="input" />
  <SearchForm.Item label="状态" name="status" inputType="select"
    options={[{ label: '启用', value: '1' }, { label: '禁用', value: '0' }]} />
</SearchForm>

<DataTable ref={tableRef} columns={columns} request={fetchData} />
```

> **注意**: `onSearch`/`onReset` 放在 SearchForm 根 props 上，不是 `submitter.onSearch`。`submitter` 仅用于按钮区渲染定制（如添加额外按钮、隐藏按钮区等），详见 `pro-patterns.md`。

## 6. Pro 输入组件可独立使用

Email、Phone、Mobile、Identity、InputMultilang 等 Pro 组件不限于在 DataForm/SearchForm 内使用，可直接在 Form.Item 中作为自定义表单控件：

```jsx
import { Email, Mobile } from 'tne-tinpernextpro-fe';

<Form.Item label="邮箱" name="email">
  <Email check emailDomainList={['@company.com', '@gmail.com']} />
</Form.Item>

<Form.Item label="手机号" name="mobile">
  <Mobile countryCode={86} />
</Form.Item>
```
