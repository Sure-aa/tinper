---
tags:
  - TinperNextPro
  - ProConfigProvider组件
---
# ProConfigProvider 全局配置

<!--ProConfigProvider-->
## API

### 功能介绍

ProConfigProvider 是 Pro 组件库的配置中心，用于全局配置 Pro 组件库的默认属性。

核心功能为：
- `多语言加载`：(基于tne-core-fe/i18n进行封装，内置多语请求等逻辑处理)
1. 本地资源渲染（或者专属化渲染）：需要将本地 src/i18n 多语内容加载到 I18nProvider 属性传入即可。
2. 线上资源加载：需要额外传入多语分组编码 groupCode 作为多语加载参数，租户以及语种会根据上下文等逻辑默认获取。
3. 自定义多语加载 hook - getRemoteResources，请求自定义多语。
4. 脱离工作台，自己切换多语，需要配置 locale 属性设置当前语言，pack 本地语料，或者 getRemoteResources，请求自定义多语。

- `表单布局`layout根据语言默认配置布局
    - 首先以用户传入为优先级最高，。
    - 用户不传入，则中繁日韩四种语言认为中语系，layout为 horizontal，其余为 vertical


获取`语言`逻辑顺序和tne-core-fe/i18n保持一致,顺序如下：
1. url query中locale参数
2. window.cb.globalization.locale
3. window.globalization.locale
4。diworkContext上下文
5. cookie locale字段
6. 浏览器语言
7. zh_CN


### Props 属性

| **属性**           | **解释**                                                                    | 属性类型                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| pack               | 本地多语包.如果只用线上，可不传 。                                          | Object {zhcn:{UID:P_GZTEVENT_178FD7A004780072:"请输入事件类型名称"},zhtw:{UID:P_GZTEVENT_178FD7A004780072:"請輸入事件類型名稱"}} |
| locale             | 设置当前语言。可不传递，内置语言获取逻辑，如有自定义需求，可传递                                                       | string /参考ConfigProvider locale字段说明                                                                                                                          |
| getRemoteResources | 如果存在一部分自定义请求多语，用此方法，返回 Promise,结果为多语 Pack 包结构(参数为configProvider传入的配置) | (config)=>Promise（结构和 pack 属性一致）                                                                                              |
| groupCode          | 在线多语加载分组编码，多个分组用英文逗号分隔                                                            | string                                                                                                                           |
| tenantId           | 租户 id.默认在工作台中会获取，可不传。如想要调试，可手动传入。              | string /0                                                                                                                          |
| url                | 请求多语地址，默认为/iuap-apcom-i18n，可不传。                              | string                                                                                                                           |


其余属性，则继承自基础组件ConfigProvider.