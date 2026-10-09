---
tags:
  - TinperNextPro
  - SearchForm组件
---
# SearchForm 查询表单

## 自定义提交区域按钮
继承于TinperNext-Form组件。

```tsx
import React from "react";
import { Button, Space } from "@tinper/next-ui";
import { SearchForm } from "tne-tinpernextpro-fe";

const SubmitterSearchForm2 = () => {
  const formRef = React.useRef(null);
  const onSearch = (values: any, errors: any, formIns: any) => {
    console.log("onSearch获取到的form实例", formIns);
    console.log("onSearch获取到的{key:value}格式表单值", values);
    console.log("onSearch捕获到的表单错误信息", errors);
  };
  const onReset = (values: any, formIns: any) => {
    console.log("onReset", values, formIns);
  };
  return (
    <>
      <Space className={"demo-wrap--list--buttons"}></Space>
      <h5>自定义提交区域按钮，表单项少于3个按钮跟随</h5>
      <SearchForm
        ref={formRef}
        onReset={onReset}
        onSearch={onSearch}
        key="submitter-demo-search-form1"
        submitter={{
          spaceProps: {
            size: "small",
          },
          submitButtonProps: {
            type: "default",
          },
          render (_props: any, dom: any) {
            return [
              ...dom,
              <Button
                onClick={() => {
                  console.log("点击了自定义1按钮");
                }}
              >
                自定义1
              </Button>,
              <Button
                onClick={() => {
                  console.log("点击了自定义2按钮");
                }}
              >
                自定义2
              </Button>,
            ];
          },
        }}
      >
        <SearchForm.Item
          inputType="input"
          label="输入框"
          name="submitter_input"
        />
        <SearchForm.Item
          inputType="number"
          label="数字框"
          name="submitter_number"
        />
      </SearchForm>
    </>
  );
};

export default SubmitterSearchForm2;
```
