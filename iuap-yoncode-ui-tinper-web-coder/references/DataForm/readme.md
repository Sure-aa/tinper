---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

<!--DataForm-->

## API

> 默认继承基础组件 Form, TinperNext 的 initialValues 和 Form api 查看[这里](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-form/bip)

| 参数          | 说明                                   | 类型                                                            | 默认值 | 版本  |
| ------------- | -------------------------------------- | --------------------------------------------------------------- | ------ | ----- |
| ref           | 表单实例，在 Form Ref 上做的封装       | FormInstance                                                    | -      | 1.0   |
| readOnly      | 是否只读                               | boolean                                                         | false  | 1.0   |
| disabled      | 是否禁用                               | boolean                                                         | false  | 1.0   |
| formLayout    | 表单列布局，默认自动，支持流式和固定列 | 'auto' \| number                                                | -      | 1.0   |
| hiddenKeys    | 隐藏的字段，依然会收集和校验字段值     | string[] \|\| {key:true\|false\|'visible'\|'hidden'\|'destroy'} | []     | 1.0   |
| invisibleKeys | 不显示的字段，不会收集和校验字段值     | string[]                                                        | []     | 1.0   |
| requiredKeys  | 必填的字段，会收集和校验字段值         | string[]                                                        | []     | 1.0   |
| disabledKeys  | 禁用的字段，依然会收集和校验字段值     | string[]                                                        | []     | 1.0   |
| values        | 完全受控的表单值，可覆盖 initialValues | {[name]: [value]}                                               | {}     | 1.0.6 |
| formMode      | 表单模式，支持编辑态、浏览态           | `edit`\|`browse`                                                | `edit` | 1.0.6 |
| labelWidth    | 自定义配置 label 宽度                  | number                                                          | 90     | 1.0.6 |

### formLayout

-   自适应：form 根据外层容器宽度所在断点区间自动设置列数
    -   label 4-6 字，1920: 5 列、1360: 4 列、1080: 3 列、600: 2 列、<600: 1 列
    -   label 8-12 字 TODO, 2200: 5 列、1600: 4 列、1080: 3 列、800: 2 列、<800: 1 列
-   固定列：表单显示固定列数

```js
/**
 * 表单列布局，默认自动，支持流式和固定列
 * 'auto' | number
 * 'auto'：自适应，根据屏宽所在断点区间自动设置列数
 *  number：固定列数
 */
formLayout?: "auto" | number;
```

### Hooks

-   除使用 Ref 外，还可以使用 Hook 获取表单实例

| 方法            | 说明                                                   | 类型                   | 默认值 | 版本 |
| --------------- | ------------------------------------------------------ | ---------------------- | ------ | ---- |
| useFormInstance | 获取当前上下文正在使用的 Form 实例，封装子组件无需透传 | () => DataFormInstance | -      | 1.0  |

-   DataForm Instance
    DataForm 与 TinperNext createForm/useForm 返回的实例不同，DataForm 实例上有以下方法

| 方法              | 说明             | 参数     | 返回值         | 版本 |
| ----------------- | ---------------- | -------- | -------------- | ---- |
| getFormContainer  | 获取表单容器宽高 | 无需传参 | {width,height} | 1.0  |
| getRequiredFields | 获取必填字段     | 无需传参 | string[]       | 1.0  |

```js
/**
 * 获取表单容器宽高
 * @params 无需传参
 * @returns {width,height}
 * 使用方式：formRef.current.getFormContainer()
 */
getFormContainer(): { width: number; height: number };
```

### FormItem 实例

> 通过 DataForm 的 ref 可以获取 Form 和所有子 FormItem 实例

## DataForm.Item

-   DataForm 自带默认的表单项，表单项组件本质上是 Form.Item 和组件的组合，我们可以当做一个 FormItem 来使用，并且支持公共 props 和各个表单项分别支持的 filedProps
-   默认继承[Form.Item](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-form/bip)
-   DataFormItem 的属性会向下透传给 FormItem，FormItem 的属性合并公共属性后向下透传给组件

-   DataFormItem 特有属性如下

| 参数          | 说明                             | 类型                               | 默认值  | 版本  |
| ------------- | -------------------------------- | ---------------------------------- | ------- | ----- |
| inputType     | 描述 UI 控件类型                 | string                             | "input" | 1.0   |
| colSpan       | 指定 FormItem 组件占用的 span 数 | ColProps                           | 空      | 1.0   |
| rowBreak      | 是否强制换行                     | boolean                            | false   | 1.0   |
| required      | 是否必填                         | 表达式() \| boolean \｜ boolean    | false   | 1.0   |
| pattern       | 正则表达式校验                   | RegExp                             | 空      | 1.0   |
| patternMsg    | 正则表达式校验失败后的错误提示   | string                             | 空      | 1.0   |
| readOnly      | 是否只读                         | 继承自 Form \| 表达式() \| boolean | false   | 1.0   |
| disabled      | 是否禁用                         | 继承自 Form \| 表达式() \| boolean | false   | 1.0   |
| rules         | 校验规则                         | Rule[]                             | 空      | 1.0   |
| previewRender | 浏览态自定义渲染函数             | function                           | --      | 1.0.6 |

-   支持的组件列表

| inputType        | 组件名           | 组件说明   | 版本 | 示例                                                                                                                                                                                                                |
| ---------------- | ---------------- | ---------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| input            | Input            | 输入框     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="输入框" inputType="input"></DataForm.Item></DataForm>                                                                                                               |
| number           | InputNumber      | 数字框     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="数字框" inputType="number"></DataForm.Item></DataForm>                                                                                                              |
| inputNumberGroup | InputNumberGroup | 数字框组   | 1.0  | <DataForm formLayout={1} ><DataForm.Item inputType="inputNumberGroup" label="数字框组" name="numbergroup" placeholder={["请输入最小值", "请输入最大值"]} required={true} rules={[{min: 100,max: 200}]}/></DataForm> |
| textarea         | Input.TextArea   | 文本域     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="文本框" inputType="textarea"></DataForm.Item></DataForm>                                                                                                            |
| search           | Input.Search     | 搜索框     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="搜索框" inputType="search"></DataForm.Item></DataForm>                                                                                                              |
| password         | Input.Password   | 密码框     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="密码框" inputType="password"></DataForm.Item></DataForm>                                                                                                            |
| date             | DatePicker       | 日期选择   | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="日期选择" inputType="date"></DataForm.Item></DataForm>                                                                                                              |
| time             | TimePicker       | 时间选择   | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="时间选择" inputType="time"></DataForm.Item></DataForm>                                                                                                              |
| rangepicker      | RangePicker      | 日期区间   | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="日期区间" inputType="rangepicker"></DataForm.Item></DataForm>                                                                                                       |
| switch           | Switch           | 开关       | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="开关" inputType="switch"></DataForm.Item></DataForm>                                                                                                                |
| select           | Select           | 下拉选     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="下拉选" inputType="select"></DataForm.Item></DataForm>                                                                                                              |
| cascader         | Cascader         | 级联       | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="级联" inputType="cascader"></DataForm.Item></DataForm>                                                                                                              |
| radiogroup       | Radio.Group      | 单选组     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="单选组" inputType="radiogroup" defaultValue={2} options={[{label:"",value:1},{label:"",value:2}]}></DataForm.Item></DataForm>                                       |
| checkboxgroup    | Checkbox.Group   | 复选组     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="复选组" inputType="checkboxgroup" options={[{value:1}]}></DataForm.Item></DataForm>                                                                                 |
| treeselect       | TreeSelect       | 树选择     | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="树选择" inputType="treeselect" treeData={[{title: 'Node1',value: '0-0',key: '0-0'}]}></DataForm.Item></DataForm>                                                    |
| imageupload      | 图片上传         | 图片上传   | 1.0  | <DataForm formLayout={1}> <DataForm.Item lable="图片上传" inputType="imageupload" label="图片上传" name="imageupload" action="upload.do"/></DataForm>                                                               |
| reftree          | 参照树           | 参照树     | 1.0  |                                                                                                                                                                                                                     |
| reftable         | 参照表格         | 参照表格   | 1.0  |                                                                                                                                                                                                                     |
| reftabletree     | 参照表格树       | 参照表格树 | 1.0  |                                                                                                                                                                                                                     |
| custom           | 自定义组件       | 自定义组件 | 1.0  | <DataForm formLayout={1} ><DataForm.Item label="自定义组件" inputType="custom" render={() => <div>自定义组件</div>}></DataForm.Item></DataForm>                                                                     |
| fileupload       | 文件上传 TODO    | 附件上传   | 1.0  |                                                                                                                                                                                                                     |
| inputmap         | 地址选择 TODO    | 地图选择   | 1.0  |                                                                                                                                                                                                                     |

> inputType 为 custom 类型时需要注意，表单控件会自动为组件添加 value、onChange，数据同步将被 Form 接管，组件需要遵循以下约定：
>
> -   提供受控属性 value 或其它与 valuePropName 的值同名的属性, 不能用控件的 value 或 defaultValue 等属性来设置表单域的值，默认值可以用 Form 里的 initialValues 来设置，需要用 setFieldsValue 来更新
> -   提供 onChange 事件或 trigger 的值同名的事件，不可以再用 onChange 来做数据收集同步，需要调用 Form 的 setFieldsValue 来触发表单域的值更新，否则表单域的值不会改变

## 样式规范

### 表单项样式

-   文本、下拉、参照组，高度不可变
-   文本域，宽度占 2-3 列，单独一行展示，行高默认 2 行，可设置 1-5 行
-   附件，宽度占 3 列，单独一行展示，80-320px 高度
-   表单组

    -   组标题，一级、二级标题
    -   组标题支持展开收起
