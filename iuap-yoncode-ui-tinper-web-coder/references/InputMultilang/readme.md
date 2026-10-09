---
tags:
  - TinperNextPro
  - InputMultilang组件
---
# InputMultilang 多语录入

<!--InputMultilang-->

## API

| 参数           | 说明                 | 类型     | 默认值                  | 版本              |
|--------------|--------------------|--------|----------------------|-------------------|
| className    | 容器样式               | string | 无                 |                 |
| modalClassname| 弹窗样式               | string | 无                |                |
| modalProps| 弹窗配置，可参考tinper的modal组件               | object | 无                |                |
| onOk         | 点击确定的钩子函数，支持异步操作          | fun    | 无               |                 |
| onCancel     | 点击取消的钩子函数          | fun    | 无               |               |
| locale       | 当前语种，不填则为工作台当前语言（如果locale不在locallist列表里则当前语种改为系统语种展示）              | string | 无                    | 
| minorLanLabel| 语种lable 例: {zh_CN: '中文', en_US: 'English'}，不填则取工作台语言设置列表             | object | 无                    |               |
| sysLocale    | 系统语种，不填则取工作台的系统语种             | string | 无                    | 否     |
| localeList   | 语言列表，支持自定义正则校验，不填则取工作台语言设置列表              | object | 无                    |                |
| onChange     | 输入框的change的钩子函数    | fun    | - | -                 |
| inputId      | input的唯一值，和 form相关联         | string | 无                    |          |
| form         |  this\.props\.form，和 inputId 相关联 | object | 无                    |     |
| isAutoComplete | 是否为自动补全模式           | bool   | false                    |                  |
| options | 自动补全传入数据, 如果isAutoComplete为true为必填           | object   | | -                 |
| required     | 是否必填               | bool   | 无                    | -                 |
| showIcon     | 是否显示图标(不启用多语时可设置false)        | bool   | true                    |                  |
| handleIconClick          | 启用showIcon时，点击图标的回调     |  string | -              |         | 
| status       | 编辑态/只读态/浏览态           | string: editor/preview/browser | preview                    |  |
| maskClosable       | 遮罩层点击是否触发关闭	    | bool | true                    |  |
| modalLocale   | modal内文字信息 eg:{title:"多语信息设置"}      | object | 无           |  |                  |  |
| maxLengthObj          | 最大输入长度 例: {zh_CN: 8, en_US: 20, zh_TW: 8}      |  object | -                |  -       | 
| isTextarea          | 输入框是否为Textarea模式      |  bool | 否               |         | 
| bordered          | 输入框bordered设置     |  string | -              |         | 
| size          | 输入框size设置     |  string | -              |         | 
| instantValidation          | 多语弹框输入框是否开启即时校验     |  bool | false              |    15.5.x     | 
