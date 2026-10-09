---
tags:
  - TinperNextPro
  - Link组件
---
# Link 超链接

## 基础组件
链接组件，支持预览态、编辑态、自定义校验等

```tsx
import { Button, Radio } from '@tinper/next-ui';
import React, { useState } from "react";
import { Link } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [size, setSize] = useState<string>('md');
  const [browser, setBrowser] = useState(false);
  const [tips, setTips] = useState("");
  const [val, setVal] = useState({
    // linkAddress: "http://www.baidu.com",
    // linkText: "百度一下"
  });

  const handleChange = value => {
    console.log("handleChange: ", value);
    setVal(value);
  };

  const handleSizeChange = (value: string) => {
    console.log("handleSizeChange: ", value);
    setSize(value);
  };

  const handleAddressChange = value => {
    console.log("handleAddressChange: ", value);
    // setVal(value);
  };

  const handleClick = value => {
    console.log("handleClick: ", value);
    // value && window.open(value)
  };

  const handleError = (value, type, rule) => {
    console.log("handleError: ", value, type, rule);
    if (type === "required") {
      setTips('网址为必填项！')
    }
  };

  const handleSuccess = value => {
    console.log("handleSuccess: ", value);
    setTips('')
  };

  return (
    <div style={{ width: '500px' }}>
      <p>基础使用</p>
      <Link
        // disabled
        bordered='bottom'
        required
        className='wui-form-item-custom-error'
        style={{ width: '500px' }}
        // requiredStyle
        // hideText
        size={size}
        browser={browser}
        tips={tips}
        addressPlaceholder = "网址链接"
        textPlaceholder = "网址名称"
        defaultAddress='http://www.baidu.com'
        defaultText='百度一下'
        value={val}
        onChange={handleChange}
        onAddressChange={handleAddressChange}
        onClick={handleClick}
        onError={handleError}
        onSuccess={handleSuccess}
      />
      <br/>
      <Radio.Group value={size} onChange={handleSizeChange}>
        <Radio.Button value='xs'>超小</Radio.Button>
        <Radio.Button value='sm'>小</Radio.Button>
        <Radio.Button value='md'>中</Radio.Button >
        <Radio.Button value='nm'>大</Radio.Button>
        <Radio.Button value='lg'>超大</Radio.Button>
        <Radio.Button value={undefined}>默认</Radio.Button>
      </Radio.Group>
      <br/>
      <Button onClick={() => setBrowser(!browser)}>切换预览</Button>
    </div>
  );
};
export default LayoutDemo;
```
