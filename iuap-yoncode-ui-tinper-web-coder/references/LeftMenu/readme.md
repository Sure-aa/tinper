---
tags:
  - TinperNextPro
  - LeftMenu组件
---
# LeftMenu 左菜单

<!--LeftMenu-->

## API

### 入参概览
```js
props={
 headerConfig: {
    model: string, // 模式，button首部显示按钮， title 首部展示文本+图标
    buttonConfig?: {
      text: string, // 按钮文本
      color: string, // 按钮颜色
      style: object, // 按钮样式
      iconName: string, // 图标的icon名
      icon?: React.ReactNode, // 图标的render函数
      onClick: ()=>void // 按钮点击回调
    },
    icon?: React.ReactNode, // 图标的图片
    iconRender?: React.ReactNode, // 首部按钮的render dom
    iconStyle?: {}, // 图标样式
    iconShadowColor?: string, // 阴影颜色
    title: string, // 标题
    iconSize: string, // 图标大小
    style: object // 首部整体样式
  },
  helpConfig: {
    onClick: ()=>void
  },
  data: (MenuData)[],
  defaultSelectedItem?: { string:any }, // 默认选中的元素
  onFoldChange: (val:boolean)=>void // 折叠触发
  canFold: boolean // 是否可以折叠菜单
  onSelect: (item: any, key: string) => void
}
```

### 参数说明
| 字段名 | 说明 | 默认值 | 参数示例 | 版本 |
|:--:|:--:|:--:|:--:|:--:|
|canFold| 控制是否可以折叠菜单|true可以折叠，false不可以折叠|--| 1.0.9 |
| data | 菜单数据 | `[]` | 见后面数据示例 |1.0.9 |
| defaultSelectedItem | 默认选中的项 |`{}`| `{ path: '/menu3' } 接受一个对象，以这个为例，它会选中path内容为/menu3的菜单。同理，如果你在每个数据项中设置了对应的key，比如你想选中key为123的菜单，也可以传入{  key: 123 }`| 1.0.9 |
|headerConfig|菜单首部配置 | 见菜单首部默认配置|| 1.0.9 |
|helpConfig|帮助配置||| 1.0.9 |
|onFoldChange|收起展开的回调函数。传入一个boolean参数给回调函数||| 1.0.9 |
|onSelect|选中菜单项的回调函数|`（item内容，菜单的key）=>{}`注意：菜单的key为菜单系统生成的，非自定义key | `(val, key) => { console.log('选中了菜单:', val, key)}`| 1.0.9 |
| extendData | 额外值传入, 需要配置extendKey使用 | `{}`| `{ unReadCount: 1 }` | 1.0.9 | 

### headerConfig(菜单首部）配置说明
| 字段名 | 说明 | 参数值 | 是否必填 | 示例 | 版本 |
|:--:|:--:|:--:|:--:|:--:|:--:|
| model	|header模式，标题模式分为按钮模式和标题模式，两种。| title(默认)或button| 必填 || 1.0.9 |
| buttonConfig| 按钮模式配置，按钮模式下必填| {} | 按钮模式下必填 | | 1.0.9 |
|icon|标题模式下，图标图片| 引入的图片对象 |非必填| | 1.0.9 |
|iconRender|标题模式下，的自定义图标render函数，当有render函数的情况，以这个render函数为准，其他对icon的控制都无效 |null | 非必填|`iconRender:(boolean)=>{}` | 1.0.9 |
|iconStyle|标题模式下，如果使用非自定义图标，则这个样式会作用到图标上|一个style对象，默认{}|非必填|| 1.0.9 |
|iconShadowColor|标题模式下，图标的阴影颜色|var(--wui-primary-color-light)。可以填写rgba等色值，如果不需要默认的阴影传入“” | 否 | | 1.0.9 |
|title| 标题模式下，标题| 应用名称|标题模式下必填| `标题` | 1.0.9 |
|iconSize|标题模式下，图标大小|默认：22px|非必填| `22px` | 1.0.9 |
|style|首部整体样式|一个style对象，默认{}|非必填| `{ background: 'white' }` | 1.0.9 |

### headerConfig.buttonConfig按钮配置和说明
| 字段名 | 说明 | 默认参数值 | 是否必填 | 版本 |
|:--:|:--:|:--:|:--:|:--:|
| text | 按钮的文字内容 | '' |  是 | 1.0.9 |
| color | 按钮的文字颜色 | 'white' | 否 |  1.0.9 |
| style | 按钮的style样式 | {} | 否 | 1.0.9 | 
| iconName | tinper的图标名, 在icon字段之间二选一，优先icon字段 | '' | 否 | 1.0.9 | 
| icon | 图标的render函数 | null |  否 | 1.0.9 | 
| onClick | 点击按钮之后的回调 | ()=> {} | 否 | 1.0.9 | 

### 菜单data属性数据示例
> data接受2层数组结构，见如下示例。内层数组为每组菜单数据，外层数组为组。

#### 菜单数据项API
| 字段名 | 说明 | 示例 | 版本 |
|:--:|:--:|:--:|:--:|
| text | 菜单文本 | `'菜单'` | 1.0.9 |
| iconName | 图标展示，使用tinper图标可以直接写名称 | `'uf-cloud'` | 1.0.9 |
| iconRender | 使用render的方式渲染图标，优先级高于iconName，激活状态会通过Boolean值作为参数传入render函数 | `(isActive) => { return <span style={{ color: isActive ? 'red' : 'black' }}>A</span> }` | 1.0.9 |
| children | 子菜单，目前只支持一层children | [] | 1.0.9 |
| extendKey | 额外值 | 通过这个参数可以设置extendData接受到额外的内容，展示在菜单项的最右边 | 1.0.9 |


```jsx
// 菜单数据
// 第一组
const data1 = [
  {
    text: '菜单1',
    // iconName: 'uf-cloud' // 支持tinper的icon的名称
    iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'black' }}>A</span> }
  },
  {
    text: '菜单2',
    // iconName: 'uf-folder',
    children: [
      {
        // iconName: 'uf-cloud', // 支持tinper的icon的名称
        // render方式
        iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'black' }}>abc</span> },
        text: '菜单2-1'
      }
    ]
  }
]
// 第二组
const data2 = [
  {
    text: '菜单3',
    iconName: '',
    path: '/menu3'
  },
  {
    text: '菜单4',
    // iconName: 'uf-folder', // 支持tinper的icon的名称
    children: [
      {
        iconName: 'uf-cloud',
        text: '菜单4-1'
      }
    ]
  }
]
// 真正的data内容
const data = [
  data1, data2
]
````

## 菜单首部默认配置示例

```js
{
  model: 'title', // title | button
  // 标题模式下不用配置buttonConfig
  buttonConfig: {
    text: '主按钮',
    color: 'white',
    style: {},
    // iconName: 'icon-ec-commonadd', // 按钮图标文本
    icon: null, // 图标的元素
    onClick: () => { }
  },
  icon: demoIcon, // 首部按钮图标
  title: '应用名称', // 首部的文本
  iconSize: '22px', // 图标大小
  iconStyle: {}, // 顶部icon的样式
  iconShadowColor: 'var(--wui-primary-color-light)', // 图标阴影
  style: {} // 首部模块的样式
}
```