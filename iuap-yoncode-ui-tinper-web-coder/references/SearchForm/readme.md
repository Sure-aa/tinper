---
tags:
  - TinperNextPro
  - SearchForm组件
---
# SearchForm 查询表单

<!--SearchForm-->
## API
> 默认继承[DataForm](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-form/bip)

| 参数             | 说明                                   | 类型                                                                                     | 默认值            | 版本 |
| ---------------- | -------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------- | ---- |
| formLayout       | 表单列布局，默认自动，支持流式和固定列 | 'auto' \| number                                                                         | -                 | 1.0  |
| collapsedNumber  | 折叠时显示的行数                       | number                                                                                   | 1                 | 1.0  |
| defaultCollapsed | 默认是否折叠                           | boolean                                                                                  | true              | 1.0  |
| onCollapse       | 折叠回调                               | function                                                                                 | (collapsed)=>void | 1.0  |
| configurable     | 是否开启高级设置 TODO                  | boolean                                                                                  | false             | 1.0  |
| searchType       | 查询表单类型                           | 'simple' \| 'normal'                                                                     | 'normal'          | 1.0  |
| submitter        | 提交按钮配置                           | boolean \| SubmitterProps                                                                | true              | 1.0  |
| onSearch         | 查询方法，直接传给 SearchForm 根属性   | `(values, errors, {changedValue, formRef, isReset})=>void`                                | -                 | 1.0  |
| onReset          | 重置方法，直接传给 SearchForm 根属性   | `(values, formIns)=>void`                                                                 | -                 | 1.0  |
| contentRender    | 自定义内容渲染                         | (items: React.ReactNode[],submitter: React.ReactElement \| undefined) => React.ReactNode | -                 | 1.0  |
| showSelected    | 是否显示已选条件，默认为true                         | boolean | true                | 1.0.5  |
| instant    | 是否开启实时搜索，开启后条件改变会触发onSearch事件                        | boolean | false                | 1.0.6  |


## SubmitterProps

- 描述查询表单的提交区域渲染
- submitter 为 false 时，不渲染提交区域
- searchType 为 simple 时，不渲染提交区域

| 参数              | 说明                         | 类型                                                                                    | 默认值 | 版本 |
| ----------------- | ---------------------------- | --------------------------------------------------------------------------------------- | ------ | ---- |
| searchConfig      | 搜索的配置，一般用来配置文本 | `{resetText='查询',submitText='清空'}`                                                  | -      | 1.0  |
| spaceProps        | 间距配置的 props             | [SpaceProps](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-space/other)   | -      | 1.0  |
| submitButtonProps | 提交按钮的 props             | [ButtonProps](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-button/other) | -      | 1.0  |
| resetButtonProps  | 重置按钮的 props             | [ButtonProps](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-button/other) | -      | 1.0  |
| render            | 自定义操作的渲染             | `false` \| `(props,dom:JSX[])=>ReactNode[]`                                             | -      | 1.0  |

> `submitter` 只负责提交区域渲染。`onSearch` 和 `onReset` 必须放在 SearchForm 根属性。render 的第二个参数是默认的 dom 数组，第一个是重置按钮，第二个是提交按钮。

## SearchForm 根回调类型

```js
/**
 * onSearch 查询方法
 * @param values 表单值
 * @param errors 表单错误
 * @param formIns 表单实例
 * @returns void
 */
onSearch?: (values: any, errors: any, formIns: DataFormInstance) => void;

/**
 * onReset 重置方法
 * @param values 表单值
 * @param formIns 表单实例
 * @returns void
 */
onReset?: (values: any, formIns: DataFormInstance) => void;

/**
 * render 自定义操作的渲染
 * @param props <SubmitterProps>
 * @param doms 默认的dom数组，第一个是重置按钮，第二个是提交按钮
 * @returns ReactNode[] | ReactNode | false
 *
 */
render?: (props: DataFormInstance, doms: JSX.Element[]) => React.ReactNode[];

```

## SearchForm.Item

- 默认继承[DataForm.Item](https://yondesign.yonyoucloud.com/website/#/detail/component/wui-form/bip)
- 特有属性如下：

| 参数         | 说明       | 类型               | 默认值 | 版本 |
| ------------ | ---------- | ------------------ | ------ | ---- |
| compareLogic | 逻辑运算符 | string \| string[] | - |1.0    |
| selectedRender | 自定义控件已选条件的渲染方式 | (val, info) => ReactNode | - | 1.0.4    |
| selectClosable | 已选条件是否可关闭 | boolean | true | 1.0.4    |

## API

- 除使用 Ref 外，还可以使用 Hook 获取查询表单实例

| 方法                  | 说明             | 类型                   | 默认值 | 版本 |
| --------------------- | ---------------- | ---------------------- | ------ | ---- |
| useSearchFormInstance | 获取查询表单实例 | ()=>SearchFormInstance | -      | 1.0  |

- SearchForm Instance
  SearchForm 与 TinperNext createForm/useForm 返回的实例不同，SearchForm 实例除继承 DataForm 实例， 实例上有以下方法

| 方法             | 说明             | 参数     | 返回值                                                                                                                   | 版本 |
| ---------------- | ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------------ | ---- |
| getFormContainer | 获取表单容器宽高 | 无需传参 | {width,height}                                                                                                           | 1.0  |
| collapsedConfig  | 折叠配置         | 无需传参 | {collapsed: boolean; collapsedLinesNumber: number; responCol: number; showCollapsed: boolean; collapsedNailed: boolean;} | 1.0  |

> 其他方法与 SearchForm 实例方法一致，具体 API 参考[SearchForm]

- SearchForm 组件继承 DataForm 组件，具体 API 参考[DataForm]

| 方法                | 说明                         | 类型                                                                                                                            | 默认值 | 版本 |
| ------------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------ | ---- |
| onSearch            | 通过方法调用表单的查询方法   | 方法调用 props.onSearch                                                                                                         | -      | 1.0  |
| onReset             | 通过方法调用表单的重置方法   | 方法调用 props.onReset                                                                                                          | -      | 1.0  |
| getFieldsLogicValue | 获取带逻辑运算符的表单值     | `()=>{name:string, value:any, compareLogic: string}[]`                                                                          | -      | 1.0  |
| getFieldLogicValue  | 获取单个带逻辑运算符的表单值 | `(name:string)=>{name:string, value:any, compareLogic: string}`                                                                 | -      | 1.0  |
| getCollapsedConfig  | 获取折叠配置                 | `()=>{ collapsed: boolean; collapsedLinesNumber: number; responCol: number; showCollapsed: boolean; collapsedNailed: boolean;}` | -      | 1.0  |
| setCollapsed        | 设置折叠状态                 | `(collapsed:boolean)=>void`                                                                                                     | -      | 1.0  |
| setShowCollapsed    | 设置是否显示折叠按钮区域     | `(showCollapsed:boolean)=>void`                                                                                                 | -      | 1.0  |
| setCollapsedNailed  | 设置是否固定折叠按钮区域     | `(collapsedNailed:boolean)=>void`                                                                                               | -      | 1.0  |

```js
/**
 * getFieldsLogicValue 获取带逻辑运算符的表单值
 * @params 无需传参
 * @returns {name:string, value:any, compareLogic: string}[]
 */
getFieldsLogicValue: () => {
  name: string;
  value: any;
  compareLogic: string;
}[];

/**
 * getFieldLogicValue 获取单个带逻辑运算符的表单值
 * @params name:string
 * @returns {name:string, value:any, compareLogic: string}
 */
getFieldLogicValue: (name: string) => {
  name: string;
  value: any;
  compareLogic: string;
};

/**
* getCollapsedConfig 获取折叠配置
* @params 无需传参
* @returns { collapsed: boolean; collapsedLinesNumber: number; responCol: number; showCollapsed: boolean; collapsedNailed: boolean;}
* collapsed 折叠状态
* collapsedLinesNumber 折叠时显示的行数
* responCol 显示的列数
* showCollapsed 是否显示折叠按钮区域
* collapsedNailed 是否固定折叠按钮区域
*/
getCollapsedConfig = () => {
  collapsed: boolean;
  collapsedLinesNumber: number;
  responCol: number;
  showCollapsed: boolean;
  collapsedNailed: boolean;
};

/**
 * setCollapsed 设置折叠状态
 * @params collapsed:boolean
 * @returns void
 */
setCollapsed = (collapsed: boolean) => void;

/**
 * setShowCollapsed 设置是否显示折叠按钮区域
 * @params showCollapsed:boolean
 * @returns void
 */
setShowCollapsed = (showCollapsed: boolean) => void;

/**
 * setCollapsedNailed 设置是否固定折叠按钮区域
 * @params collapsedNailed:boolean
 * @returns void
 */
setCollapsedNailed = (collapsedNailed: boolean) => void;

```
## fieldid
| 格式 | 说明 |
| --- | --- |
| fieldid_submit | 搜索按钮 |
| fieldid_reset | 重置按钮 |
| fieldid_submitter | 提交区域 |
| fieldid_collapse | 折叠按钮 |
| fieldid_nail | 固定按钮 |
