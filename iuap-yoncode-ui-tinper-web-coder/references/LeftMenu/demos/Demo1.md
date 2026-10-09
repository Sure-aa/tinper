---
tags:
  - TinperNextPro
  - LeftMenu组件
---
# LeftMenu 左菜单

## LeftMenu的标题模式展示
下面例子中展示了LeftMenu的标题模式展示，通过headerConfig配置标题的样式。

```jsx
import React, { useEffect, useState, useRef } from 'react';
import { LeftMenu } from 'tne-tinpernextpro-fe';

const demoIcon = require('./images/demo-header.png')

// 菜单数据
const data1 = [
  {
    text: '菜单1',
    iconName: 'uf-cloud'
    // iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'black' }}>A</span> }
  },
  {
    text: '菜单2',
    // iconName: 'icon-ec-commona-humangroup',
    children: [
      {
        iconName: 'uf-cloud',
        // render方式
        // iconRender: (isActive) => { return <span style={{ color: isActive ? 'red' : 'black' }}>abc</span> },
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
    iconName: 'uf-folder',
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
    model: 'title', // 模式，button首部显示按钮， title 首部展示文本+图标
    icon: demoIcon, // 首部按钮图标
    // iconRender: () => {
    //   return <img src={demoIcon} alt="" />
    // },
    title: '应用名称2', // 首部的文本
    iconSize: '22px', // 图标大小
    iconShadowColor: 'var(--wui-primary-color-light)', // 图标阴影颜色控制
    style: {} // 首部模块的样式
  });
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
          unReadCount
        }}
        helpConfig={{ onClick: () => {
          window.alert('点击了帮助！')
        } }} data={data} headerConfig={headerConfig} defaultSelectedItem={defaultSelectedItem} canFold={canFold}></LeftMenu>
      <div style={{ flex: 1, height: '100%', background: 'white' }}>
        <button onClick={() => changeDefault({ text: '菜单2-1' })}>设置菜单2-1激活</button>
        <button onClick={() => changeDefault({ path: '/menu3' })}>设置menu3激活</button>
        <button onClick={() => setCanFold(!canFold)}>切换是否允许收起</button>
        <button onClick={() => { setUnReadCount('99+') }}>设置未读数99+</button>
      </div>
    </div>
  )
}

export default LeftMenuDemo
```
