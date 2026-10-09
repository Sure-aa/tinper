---
tags:
  - TinperNextPro
  - Link组件
---
# Link 超链接

## 基础组件
链接组件，支持预览态、编辑态、自定义校验等

```tsx
import { Form } from '@tinper/next-ui';
import React, { useState } from "react";
import { Link } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const [browser, setBrowser] = useState(false);
  const [tips, setTips] = useState("");
  const [val, setVal] = useState({
    linkAddress: "http://www.baidu.com",
    linkText: "百度一下"
  });

  const handleChange = value => {
    console.log("handleChange: ", value);
    setVal(value);
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
    <>
      <p>样式</p>
      <Form>
        <Form.Item label='error样式' >
          <Link className='wui-form-item-custom-error' bordered='bottom' style={{ width: '500px' }} value={val}/>
        </Form.Item>

        <br></br>

        <Form.Item label='必填' >
          <Link className='wui-form-item-custom-required' bordered='bottom' style={{ width: '500px' }} value={val} />
        </Form.Item>

        <br></br>

        <Form.Item label='只读' >
          <Link readOnly style={{ width: '500px' }} value={val} />
        </Form.Item>

        <br></br>

        <Form.Item label='只读' >
          <Link readOnly bordered='bottom' style={{ width: '500px' }} value={val} />
        </Form.Item>
      </Form>
    </>
  );
};
export default LayoutDemo;
```
