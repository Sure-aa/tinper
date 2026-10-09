---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 跨列/换行表单
继承于TinperNext-Form组件。

```js
import React, { useRef } from "react";
import { DataForm } from "tne-tinpernextpro-fe";
import { Space, Button } from "@tinper/next-ui";

const ColSpanDemo = () => {
  const formRef = useRef(null);
  const formItemLayout = {
    labelCol: {
      span: 4
    },
    wrapperCol: {
      span: 12
    }
  };
  return (
    <>
      <p>跨列/换行表单</p>
      <Space className={"demo-wrap--list--buttons"}></Space>
      <div>
        <DataForm ref={formRef} key="layout-demo-form" formLayout={4}>
          <DataForm.Item
            inputType={"input"}
            label={"输入框"}
            name={"input"}
            colSpan={12}
          />
          <DataForm.Item inputType="number" label="数字框" name="demo3-number" />
          <DataForm.Item inputType="search" label="搜索框" name="demo3-search" />
          <DataForm.Item inputType="select" label="下拉框" name="demo3-select" />
          <DataForm.Item
            inputType="cascader"
            label="级联选择"
            name="demo3-cascader"
            rowBreak={true}
          />
          <DataForm.Item inputType="password" label="密码框" name="demo3-password" />
          <DataForm.Item
            inputType="date"
            label="日期选择"
            name="demo3-date"
            rowBreak={true}
          />
          <DataForm.Item inputType="time" label="时间选择" name="demo3-time" />
          <DataForm.Item
            inputType="rangepicker"
            label="日期范围"
            name="demo3-range"
            rowBreak={true}
          />
          <DataForm.Item inputType="switch" label="开关" name="demo3-switch" />
          <DataForm.Item
            inputType="checkboxgroup"
            label="复选框组"
            name="demo3-check"
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
            name="demo3-radio"
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
            name="demo3-textarea"
            colSpan={24}
          />
        </DataForm>
      </div>
    </>
  );
};
export default ColSpanDemo;
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
