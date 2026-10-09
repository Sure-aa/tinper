---
tags:
  - TinperNextPro
  - LeftMenu组件
---
# LeftMenu 左菜单

## LeftMenu的菜单项后缀控制extendData和extendKey
下面例子中展示用extendKey，在菜单项后添加extendKey绑定一个key值，然后在LeftMenu通过extendData属性，将key的值传入，即可将后缀内容与菜单进行关联，需要展示后缀的菜单需要把extendKey绑定到菜单项上。

```jsx
import React, { useEffect, useState, useRef } from 'react';
import { LeftMenu } from 'tne-tinpernextpro-fe';

// 菜单数据
const data1 = [
  {
    text: '菜单1',
    // iconName: 'uf-cloud'
    iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'blue' }}>A</span> }
  },
  {
    text: '菜单2',
    children: [
      {
        // render方式
        iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'blue' }}>abc</span> },
        text: '菜单2-1',
        fieldId: '123456'
      }
    ]
  }
]
const data2 = [
  {
    text: '菜单3',
    iconName: '',
    path: '/menu3',
    extendKey: 'unReadCount' // 添加额外传值的key
  },
  {
    text: '菜单4',
    fieldId: '1234567',
    children: [
      {
        iconName: 'uf-cloud',
        text: '未读数量',
        extendKey: 'unReadCount' // 添加额外传值的key
      },
      {
        iconName: 'uf-cloud',
        text: '超长标题超长标题超长标题超长标题',
        extendKey: '' // 添加额外传值的key
      }
    ]
  },
  {
    text: '超长标题超长标题超长标题超长标题',
    iconName: '',
    path: '/menu4',
    extendKey: 'unReadCount' // 添加额外传值的key
  }
]
const data = [
  data1, data2
]

const LeftMenuDemo = () => {
  const [headerConfig, setHeaderConfig] = useState({
    model: 'button', // 模式，button首部显示按钮， title 首部展示文本+图标
    buttonConfig: {
      text: '主按钮',
      color: 'white',
      style: {}, // 按钮样式
      iconName: 'uf-plus', // 按钮图标文本
      icon: null, // 图标的元素
      onClick: () => {
        window.alert('您点击了主按钮')
      }
    },
  });
  // 未读数
  const [unReadCount, setUnReadCount] = useState(''); 
  // 默认选中项
  const [defaultSelectedItem, setDefaultSelectedItem] = useState({ path: '/menu3' });
  // 是否可以收起
  const [canFold, setCanFold] = useState(true);

  const demoWrap = useRef(null)

  // 用于storybook的demo内容高度撑开，正常项目中无需使用这个撑开
  useEffect(() => {
    if (demoWrap && demoWrap.current) {
      // storybook 没有父级高度，给父级一个高度
      try {
        demoWrap.current.parentElement.style.height = '100%'
      } catch (error) {
        console.log(error)
      }
    }
    return () => {
      if (demoWrap && demoWrap.current) {
        // 还原项目修改
        try {
          demoWrap.current.parentElement.style.height = 'auto'
        } catch (error) {
          console.log(error)
        }
      }
    }
  }, [])

  const changeDefault = (val) => {
    setDefaultSelectedItem(val)
  }
  return (
    <div style={{ height: '100%', display: 'flex' }} ref={demoWrap}>
      <LeftMenu
        onSelect={(val, key) => {
          console.log('选中了菜单:', val, key)
        }}
        extendData={{
          unReadCount // 传递未读数
        }}
        helpConfig={{ onClick: () => {
          window.alert('点击了帮助！')
        } }} data={data} headerConfig={headerConfig} defaultSelectedItem={defaultSelectedItem} canFold={canFold}></LeftMenu>
      <div style={{ flex: 1, height: '100%', background: 'white' }}>
        <button onClick={() => { setUnReadCount('99+') }}>设置未读数99+</button>
        <button onClick={() => { setUnReadCount('') }}>清除未读数99+</button>
      </div>
    </div>
  )
}

export default LeftMenuDemo
```
