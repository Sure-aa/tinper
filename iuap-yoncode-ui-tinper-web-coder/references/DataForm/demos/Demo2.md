---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 布局表单
继承于TinperNext-Form组件。

```js
import { Button, ConfigProvider, Radio, Space } from "@tinper/next-ui";
import React, { useRef } from "react";
import { DataForm } from "tne-tinpernextpro-fe";

const LayoutDemo = () => {
  const containerRef = useRef(null);
  const formRef = useRef(null);
  const [layout, setLayout] = React.useState("horizontal");
  const [formLayout, setFormLayout] = React.useState("auto");
  const [hidden, setHidden] = React.useState(false);
  const [zoom, setZoom] = React.useState(0.5);

  const handleChangeLayout = (value) => {
    setLayout(value);
  };

  const changeSize = () => {
    if ((containerRef.current.getBoundingClientRect().width > 1500 && zoom > 1) || (containerRef.current.getBoundingClientRect().width < 500 && zoom < 1)) {
      setZoom(1 / zoom);
    }
    containerRef.current.style.width = `${containerRef.current.getBoundingClientRect().width * zoom}px`
  }

  return (
    <>
      <p>布局表单</p>
      <Space className={"demo-wrap--list--buttons"}>
        <Radio.Group size='md' value={layout} onChange={handleChangeLayout}>
          <Radio.Button value='horizontal'>Horizontal</Radio.Button>
          <Radio.Button value='vertical'>Vertical</Radio.Button>
        </Radio.Group>

        <Button
          onClick={() => {
            setFormLayout("vertical");
          }}
        >
          上下布局
        </Button>
        <Button
          onClick={() => {
            setFormLayout("auto");
          }}
        >
          自适应布局
        </Button>
        <Button
          onClick={() => {
            setFormLayout(1);
          }}
        >
          固定单列
        </Button>
        <Button
          onClick={() => {
            setFormLayout(2);
          }}
        >
          固定两列
        </Button>
        <Button
          onClick={() => {
            setHidden(!hidden);
          }}
        >
          设置隐藏
        </Button>
        <Button onClick={changeSize}>缩放容器</Button>
      </Space>
      <ConfigProvider layout={layout}>
        <div ref={containerRef} style={{ border: '1px solid #0ff' }}>
          <DataForm ref={formRef} key="layout-demo-form" formLayout={formLayout}>
            <DataForm.Item inputType={"input"} label={"输入框"} name={"input"} />
            <DataForm.Item
              inputType="number"
              label="数字框"
              name="demo2-number"
              hidden={hidden}
            />
            <DataForm.Item inputType="search" label="搜索框" name="demo2-search" />
            <DataForm.Item inputType="select" label="下拉框" name="demo2-select" />
            <DataForm.Item inputType="password" label="密码框" name="demo2-password" />
            <DataForm.Item
              inputType="cascader"
              label="级联选择"
              name="demo2-cascader"
            />
            <DataForm.Item inputType="date" label="日期选择" name="demo2-date" />
            <DataForm.Item inputType="time" label="时间选择" name="demo2-time" />
            <DataForm.Item
              inputType="rangepicker"
              label="日期范围"
              name="demo2-range"
            />
            <DataForm.Item inputType="switch" label="开关" name="demo2-switch" />
            <DataForm.Item
              inputType="checkboxgroup"
              label="复选框组"
              name="demo2-check"
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
              name="demo2-radio"
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
            <DataForm.Item inputType="textarea" label="文本域" name="demo2-textarea" />
          </DataForm>
        </div>
      </ConfigProvider>
    </>
  );
};
export default LayoutDemo;
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
