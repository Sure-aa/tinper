---
tags:
  - TinperNextPro
  - InputMultilang组件
---
# InputMultilang 多语录入

## 多语言高级配置示例
展示多语言组件的高级配置功能，包括：单独设置字数限制、自定义校验规则，多语弹框布局等

```js
import React, { useState } from 'react';
import { Switch, ConfigProvider } from '@tinper/next-ui';
import { InputMultilang } from 'tne-tinpernextpro-fe';

const Demo3 = () => {

  const handleInputModelOk = (localeList) => {
    console.log('localeList', localeList);
    // return new Promise((resolve, reject) => {
    //   setTimeout(() => resolve(true), 1000);
    // });
  }

  const handleOnChange = (localeValue, localeList) => {
    console.log('localeValue', localeValue);
    console.log('localeList', localeList);
  }

  const handleOnBlur = (localeValue, localeList) => {
    console.log('localeValue', localeValue);
    console.log('localeList', localeList);
  }

  const handleInputFocus = (e) => {
    console.log('handleInputFocus', e);
  }

  const [instantValidation, setInstantValidation] = useState(false);
  const [layout, setLayout] = useState('horizontal');
  const props = {
    localeList: {
      "zh_CN": {
        value: '',
        maxLength: 10,
        rules: [
          {
            pattern: /^[\u4e00-\u9fa5]+$/,
            message: '只能输入中文'
          },
        ]
      },
      "en_US": {
        value: '',
        maxLength: 20,
        rules: [
          {
            pattern: /^[a-zA-Z\s]+$/,
            message: 'Only English characters allowed'
          },
          {
            required: true,
            message: 'required'
          },
        ]
      },
      "zh_TW": {
        value: '',
        maxLength: 10,
        rules: [
          {
            pattern: /^[\u4e00-\u9fa5]+$/,
            message: '只能輸入中文'
          }
        ]
      }
    },
    required: true,
    inputId: 'demo3',
    sysLocale: "en_US",
    locale: "zh_CN",
    status: 'editor',
    fieldid: 'demo3-field',
    allowClear: true,
    onChange: handleOnChange,
    onBlur: handleOnBlur,
    onOk: handleInputModelOk,
    onFocus: handleInputFocus,
    instantValidation: instantValidation,
  }

  return (
    <ConfigProvider layout={layout}>
      <div style={{ marginBottom: '10px' }}>
        <label>多语弹框输入框是否开启即时校验：</label>
        <Switch checked={instantValidation} onChange={setInstantValidation} style={{ marginRight: "10px" }} />
        <label>多语弹框布局horizontal/vertical：</label>
        <Switch checked={layout === 'vertical'} onChange={(flg) => setLayout(flg ? 'vertical' : 'horizontal')} />
      </div>
      <InputMultilang
        placeholder="请输入"
        className="input-multilang"
        modalProps={{
          centered: true,
        }}
        {...props}
      />
    </ConfigProvider>
  );
}

export default Demo3;
```
