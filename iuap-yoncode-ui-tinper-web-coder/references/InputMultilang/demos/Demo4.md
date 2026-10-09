---
tags:
  - TinperNextPro
  - InputMultilang组件
---
# InputMultilang 多语录入

## 多语配置组件基础用法
用于自定义词条多语内容的配置，录入弹框词条类型可以自定义

```js
import React from 'react';
import { Switch, Form } from '@tinper/next-ui';
import { InputMultilang } from 'tne-tinpernextpro-fe';

const Demo4 = () => {
  const [isTextarea, setIsTextarea] = React.useState(false);
  const [layout, setLayout] = React.useState('horizontal');
  const [localeList, setLocaleList] = React.useState({
    'zh_CN': 'CN',
    'en_US': 'EN',
    'zh_TW': 'TC',
    'fr_FR': 'FR',
    'de_DE': 'DE',
    'ja_JP': 'JP',
    'ko_KR': 'KO',
    'ru_RU': 'RU',
    'it_IT': 'IT',
    'pt_PT': 'PT'
  });


  const handleInputModelOk = (localeList) => {
    console.log('localeList', localeList);
    setLocaleList(localeList);
  }

  const handleOnChange = (localeValue, localeList) => {
    console.log('localeValue', localeValue);
    console.log('localeList', localeList);
    setLocaleList(localeList);
  }

  const handleOnBlur = (localeValue, localeList) => {
    console.log('localeValue', localeValue);
    console.log('localeList', localeList);
  }


  const props = {
    localeList: localeList,
    required: true,
    inputId: '123456',
    isPopConfirm: false,
    sysLocale: "en_US",
    locale: "zh_CN",
    onChange: handleOnChange,
    onBlur: handleOnBlur,
    onOk: handleInputModelOk,
    isTextarea: isTextarea,
    status: 'editor',
    layout: layout,
  }
  return (  
    <div>
      <div style={{ marginBottom: '10px' }}>
        <label style={{ display: 'inline-block' }}>改为Textarea：</label>
        <Switch
          checked={isTextarea}
          onChange={() => setIsTextarea(!isTextarea)}
          style={{ marginRight: "10px" }}
        />
        <label>多语弹框布局horizontal/vertical：</label>
        <Switch checked={layout === 'vertical'} onChange={(flg) => setLayout(flg ? 'vertical' : 'horizontal')} />
      </div>
      <InputMultilang
        placeholder="请输入"
        modalProps={{
          centered: true,
        }}
        {...props}
      />
    </div>
  );
}

export default Demo4;
```
