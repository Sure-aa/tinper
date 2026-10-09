# AutoCode 自动编码

自动编码能力用于根据业务对象、领域、服务和字段规则查询编码规则，并在新增或依赖字段变化时生成单据编号。

## 导入方式

```tsx
import {
  AutoCode,
  useAutoCode,
  createAutoCodeService,
} from 'tne-tinpernextpro-fe/supports';
```

## 推荐入口

| API | 用途 |
| --- | --- |
| `AutoCode` | 表单字段内直接渲染自动编码输入 |
| `useAutoCode` | 自定义输入 UI 时接管自动编码状态和动作 |
| `createAutoCodeService` | 接入自定义请求封装时创建服务适配器 |

工具函数如 `resolveAutoCodeMode`、`parseAutoCodeRule`、`normalizeAutoCodeValue` 主要用于高级适配或测试。

## 最小示例

```tsx
<AutoCode
  busiObj="finance.ap.bill"
  domainKey="finance"
  serviceCode="ap"
  field="code"
  mode="add"
  value={formValues.code}
  source={{
    getCurrentPageData: () => formRef.current?.getFieldsValue?.() || {},
    subscribeDependencies: (_dependencies, notify) => {
      const unsubscribe = subscribeFormChange(notify);
      return unsubscribe;
    },
  }}
  onChange={code => formRef.current?.setFieldsValue({ code })}
  onError={Message.error}
/>
```

## 关键 Props

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `source` | `AutoCodeSource` | 页面数据读取和依赖字段订阅入口，必填 |
| `busiObj` | `string` | 业务对象编码，必填 |
| `domainKey` | `string` | 领域标识，必填 |
| `serviceCode` | `string` | 服务编码 |
| `field` | `string` | 当前编码字段名 |
| `mode` | `'browse' \| 'edit' \| 'add'` | 页面模式 |
| `value` | `string \| number \| null` | 当前编码值 |
| `adapter` | `AutoCodeAdapter` | 自定义规则查询和取号服务 |
| `renderInput` | `(props) => React.ReactElement` | 自定义输入组件 |
| `onChange` | `(value: string) => void` | 编码变化回调 |
| `onError` | `(error: Error) => void` | 规则查询或取号失败回调 |

## Source 和 Adapter

```ts
type AutoCodeSource = {
  getCurrentPageData: (dependencies?: AutoCodeRuleDependency[]) => Record<string, unknown>;
  subscribeDependencies: (
    dependencies: AutoCodeRuleDependency[],
    notify: () => void,
  ) => () => void;
};

type AutoCodeAdapter = {
  queryRule: (params: AutoCodeServiceParams, data?) => Promise<AutoCodeRule | null>;
  createCode: (params: AutoCodeServiceParams, data?) => Promise<string>;
};
```

## 常见错误

- `source` 是必填核心协议；不要让 AutoCode 隐式读取业务页面状态。
- 新增、编辑、浏览态要通过 `mode` 或当前数据明确区分，避免编辑态重新取号覆盖已有编码。
- 规则依赖字段变化时通过 `subscribeDependencies` 通知组件，不要只在初始化时查一次规则。

## 源码依据

- `node_modules/tne-tinpernextpro-fe/src/supports/autoCode/docs/readme.md`
- `node_modules/tne-tinpernextpro-fe/src/supports/autoCode/src/index.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/autoCode/src/types.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/autoCode/src/useAutoCode.ts`
- `node_modules/tne-tinpernextpro-fe/src/supports/autoCode/src/service.ts`
