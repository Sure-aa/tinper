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

const Demo1 = () => {
  const [isTextarea, setIsTextarea] = React.useState(false);
  const [showIcon, setShowIcon] = React.useState(true);
  const [status, setStatus] = React.useState('editor');
  const [focusSelect, setFocusSelect] = React.useState(false);
  const [localeList, setLocaleList] = React.useState({
    "zh_CN":"test",
    "en_US":"",
    "zh_TW":""
  });
  const [modalVisible, setModalVisible] = React.useState(false);


  const handleInputModelOk = (localeList) => {
    console.log('localeList', localeList);
    setLocaleList(localeList);
    setModalVisible(false);
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

  const handleInputFocus = (e) => {
    console.log('handleInputFocus', e);
  }

  const handleIconClick = (e) => {
    console.log('handleIconClick', e);
    setModalVisible(true);
  }

  const handleOnCancel = (form) => {
    console.log('handleOnCancel', form);
    setLocaleList({
      "zh_CN":"",
      "en_US":"",
      "zh_TW":""
    });
    form.resetFields();
    setModalVisible(false);
  }


  const props = {
    localeList: localeList,
    required: true,
    inputId: '123456',
    isPopConfirm: false,
    sysLocale: "en_US",
    locale: "zh_CN",
    status: status,
    fieldid: 'test',
    onChange: handleOnChange,
    onBlur: handleOnBlur,
    onOk: handleInputModelOk,
    onFocus: handleInputFocus,
    isTextarea: isTextarea,
    showIcon: showIcon,
    focusSelect: focusSelect,
    handleIconClick: handleIconClick,
    onCancel: handleOnCancel,
    status: status,
    // maxLengthObj: {'zh_CN': 8, 'en_US': 20, 'zh_TW': 8}  // 最大长度限制旧版本写法
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
        <label style={{ display: 'inline-block' }}>是否显示多语图标：</label>
        <Switch
          checked={showIcon}
          onChange={() => setShowIcon(!showIcon)}
          style={{ marginRight: "10px" }}
        />
        <label style={{ display: 'inline-block' }}>是否为只读态：</label>
        <Switch
          checked={status === 'preview'}
          onChange={() => setStatus(status === 'editor' ? 'preview' : 'editor')}
          style={{ marginRight: "10px" }}
        />
        <label style={{ display: 'inline-block' }}>是否为浏览态：</label>
        <Switch
          checked={status === 'browser'}
          onChange={() => setStatus(status === 'editor' ? 'browser' : 'editor')}
          style={{ marginRight: "10px" }}
        />
        <label style={{ display: 'inline-block' }}>内容区是否聚焦选中：</label>
        <Switch
          checked={focusSelect}
          onChange={() => setFocusSelect(!focusSelect)}
          style={{ marginRight: "10px" }}
        />
      </div>
      <InputMultilang
        placeholder="请输入"
        className="input-multilang"
        modalProps={{
          centered: true,
          visible: modalVisible,
        }}
        {...props}
      />
    </div>
  );
}

export default Demo1;
```
