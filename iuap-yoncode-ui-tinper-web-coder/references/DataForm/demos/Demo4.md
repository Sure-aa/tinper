---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 校验表单
继承于TinperNext-Form组件。

```js
import { Button, Space } from "@tinper/next-ui";
import React, { useRef } from "react";
import { DataForm } from "tne-tinpernextpro-fe";

const ValidateDemo = () => {
  const formRef = useRef(null);
  const [requiredKeys, setRequiredKeys] = React.useState(["input"]);
  const userNameReg = (_rule, value, callback) => {
    const reg = /^[a-zA-Z0-9\u4e00-\u9fa5][_a-zA-Z0-9\u4e00-\u9fa5]*$/g;
    if (!value) {
      callback("不能为空");
    } else if (!reg.test(value)) {
      callback("仅支持汉字/字母/数字/下划线，不能以下划线开头");
    } else if (value.length > 5) {
      callback("不能超过5个字符");
    } else {
      callback();
    }
  };
  const setRequiredFields = () => {
    setRequiredKeys(["number", "select", "password", "cascader"]);
  }
  const getRequiredFields = () => {
    console.log("getRequiredFields-->", formRef.current.getRequiredFields());
    // console.log("getFieldInstance-->", formRef.current.getFieldInstance('user'));
  };
  return (
    <>
      <p>校验表单</p>
      <Space className={"demo-wrap--list--buttons"}>
        <Button
          onClick={() => {
            formRef.current.validateFields().then((values) => {
              console.log("values-->", values);
            });
          }}
        >
          表单校验
        </Button>
        <Button
          onClick={() => {
            getRequiredFields();
          }}
        >
          获取必填项
        </Button>
        <Button
          onClick={() => { setRequiredFields() }}
        >
          设置必填项
        </Button>
        <Button
          onClick={() => {
            formRef.current.resetFields(['input', 'demo4-number'] /** 可传入数组，指定要reset的字段，如不传，则全部reset */);
          }}
        >
          重置表单(仅用户名、数字框)
        </Button>
      </Space>
      <DataForm
        ref={formRef}
        key="validate-demo-form"
        requiredKeys={requiredKeys}
        initialValues={{
          input: '悟空～～',
          'demo4-number': 111,
          'demo4-search': '搜索内容'
        }}
        locale='en-us'
      >
        <DataForm.Item
          inputType={"input"}
          label={"用户名"}
          name={"input"}
          placeholder="仅支持汉字/字母/数字/下划线"
          validateTrigger="onChange"
          required={true}
          pattern={/^[a-zA-Z0-9\u4e00-\u9fa5][_a-zA-Z0-9\u4e00-\u9fa5]*$/g}
        />
        <DataForm.Item
          inputType="number"
          label="数字框"
          name="demo4-number"
          rules={[
            {
              required: true,
              message: "请输入数字"
            }
          ]}
        />
        <DataForm.Item
          inputType="search"
          label="搜索框"
          name="demo4-search"
          required
        />
        <DataForm.Item inputType="select" label="下拉框" name="demo4-select" />
        <DataForm.Item inputType="password" label="密码框" name="demo4-password" />
        <DataForm.Item inputType="cascader" label="级联选择" name="demo4-cascader" />
        <DataForm.Item inputType="date" label="日期选择" name="demo4-date" required />
        <DataForm.Item inputType="time" label="时间选择" name="demo4-time" required />
        <DataForm.Item
          inputType="rangepicker"
          label="日期范围"
          name="demo4-range"
          required
        />
        <DataForm.Item inputType="switch" label="开关" name="demo4-switch" required />
        <DataForm.Item
          inputType="checkboxgroup"
          required
          label="复选框组"
          name="demo4-check"
          options={[
            {
              label: "选项1",
              value: "1"
            },
            {
              label: "选项2",
              value: "2"
            },
            {
              label: "选项3",
              value: "3"
            }
          ]}
        />
        <DataForm.Item
          inputType="radiogroup"
          label="单选框组"
          name="demo4-radio"
          required
          options={[
            {
              label: "选项1",
              value: "1"
            },
            {
              label: "选项2",
              value: "2"
            },
            {
              label: "选项3",
              value: "3"
            }
          ]}
        />
        <DataForm.Item
          inputType="textarea"
          label="文本域"
          name="demo4-textarea"
          required
        />
        <DataForm.Item
          inputType="inputNumberGroup"
          label="数字框组"
          name="numbergroup"
          placeholder={["请输入最小值", "请输入最大值"]}
          rules={[
            { required: true },
            {
              validator: (rule, value, callback) => { // 最大值最小值校验
                if (value && value.length > 0) {
                  if (!value[0] && value[0] !== 0) {
                    callback(`最小值为必填项`);
                  }
                  if (!value[1] && value[1] !== 0) {
                    callback(`最大值为必填项`);
                  }
                  if (value[0] < 0) {
                    callback("最小值不能小于0");
                  } else if (value[1] > 100) {
                    callback("最大值不能大于100");
                  } else if (value[0] > value[1]) {
                    callback("最小值不能大于最大值");
                  } else {
                    callback();
                  }
                } else {
                  callback();
                }
              }
            }
          ]}
        />
      </DataForm>
    </>
  );
};
export default ValidateDemo;
```

```less
.demo5-wrapper .wui-collapse-group {
    width: 100%;
    .wui-collapse-body:before,
    .wui-collapse-body::before,
    .wui-collapse-body:after,
    .wui-collapse-body::after {
        clear: both;
    }

    .wui-input-number-group {
        line-height: 0;
    }
}

```
