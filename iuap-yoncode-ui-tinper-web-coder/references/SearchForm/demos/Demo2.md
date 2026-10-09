---
tags:
  - TinperNextPro
  - SearchForm组件
---
# SearchForm 查询表单

## 默认展开表单
继承于TinperNext-Form组件。

```tsx
import React from "react";
import { Space, Button } from "@tinper/next-ui";
import { SearchForm } from "tne-tinpernextpro-fe";

const CollapsedSearchFormDemo1 = () => {
  const formRef = React.useRef(null);
  const [width, setWidth] = React.useState('100');
  const onSearch = (values: any, errors: any, formIns: any) => {
    console.log("onSearch获取到的form实例", formIns);
    console.log("onSearch获取到的{key:value}格式表单值", values);
    console.log("onSearch捕获到的表单错误信息", errors);
  };
  const onReset = (values: any, formIns: any) => {
    console.log("onReset", values, formIns);
  };

  const handleZoomClick = () => {
    // this.
    if (width > 50) {
      setWidth(width * 0.8)
    }
  };

  const handleResetClick = () => {
    setWidth(100);
  }

  return (
    <div style={{ width: `${width}%` }}>
      <Space style={{ marginBottom: '10px' }}>
        <Button onClick={handleZoomClick}>缩放容器</Button>
        <Button onClick={handleResetClick}>重置容器</Button>
      </Space>
      <SearchForm
        ref={formRef}
        onReset={onReset}
        onSearch={onSearch}
        defaultCollapsed={false}
        key="basic-demo-search-form"
      >
        <SearchForm.Item
          inputType={"input"}
          label={"输入框"}
          name={"input_collapsed1"}
        />
        <SearchForm.Item
          inputType="rangepicker"
          label="数字框"
          rowBreak
          name="number_collapsed1"
        />
        <SearchForm.Item
          inputType="search"
          label="搜索框"
          name="search_collapsed1"
        />
        <SearchForm.Item
          inputType="select"
          label="下拉框"
          name="select_collapsed1"
        />
        <SearchForm.Item
          inputType="cascader"
          label="级联选择"
          name="cascader_collapsed1"
        />
        <SearchForm.Item
          inputType="date"
          label="日期选择"
          name="date_collapsed1"
        />
        <SearchForm.Item
          inputType="time"
          label="时间选择"
          name="time_collapsed1"
        />
        <SearchForm.Item
          inputType="rangepicker"
          label="日期范围"
          name="range_collapsed1"
        />
        <SearchForm.Item
          inputType="checkboxgroup"
          label="复选框组"
          name="check_collapsed1"
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
        <SearchForm.Item
          inputType="radiogroup"
          label="单选框组"
          name="radio_collapsed1"
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
      </SearchForm>
    </div>
  );
};
export default CollapsedSearchFormDemo1;
```
