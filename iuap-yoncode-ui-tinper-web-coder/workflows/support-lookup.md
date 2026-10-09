# 支撑服务查询工作流

当问题涉及 NextPro 支撑服务时，按以下顺序查证：

1. 查 `../quickref/supports-router.md` 判断模块。
2. 查 `../references/supports/<module>.md` 获取推荐入口、参数和常见错误。
3. 页面组合问题查 `../patterns/support-patterns.md`。
4. 报错、运行时、接入边界问题查 `../gotchas/support-gotchas.md`。
5. 文档缺失或矛盾时查源码：`node_modules/tne-tinpernextpro-fe/src/supports/<module>/src`。

源码查证优先级：

| 顺序 | 文件 | 用途 |
| --- | --- | --- |
| 1 | `src/index.ts` / `src/index.tsx` | 确认真实导出 |
| 2 | `src/types.ts` 或 `src/iMdf*.ts` | 确认参数、返回值和类型 |
| 3 | Hook / service / runtime 文件 | 确认行为和默认值 |
| 4 | `demo/*.tsx` | 提取最小可用示例 |
| 5 | `__tests__/*` | 确认边界行为和回归规则 |

回答时说明使用了哪个支撑服务入口，并明确业务侧需要传入哪些上下文或 facade 方法。
