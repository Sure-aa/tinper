---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 基础数据表单
继承于TinperNext-Form组件。

```js
import React, { useRef } from "react";
import { DataForm } from "tne-tinpernextpro-fe";
import {
  Space,
  Radio
} from "@tinper/next-ui";

// const sights = ["tianjinfan", "Great Wall"];

const BasicDemo = () => {
  const formRef = useRef(null);
  //   const [val, setVal] = useState("");
  const onValuesChange = (props, changed) => {
    console.log("FormValueChange-->", props, changed);
  };
  const onFieldsChange = (props, changed) => {
    console.log("FieldsChange-->", props, changed);
  };
  //   const formItemLayout = {
  //     labelCol: {
  //       span: 4,
  //     },
  //     wrapperCol: {
  //       span: 12,
  //     },
  //   };
  //   const [matchData, setMatchData] = React.useState([]);
  return (
    <>
      <Space className={"demo-wrap--list--buttons"}></Space>
      <div
        style={{
          width: "50%"
        }}
      >
        <DataForm
          ref={formRef}
          onValuesChange={onValuesChange}
          onFieldsChange={onFieldsChange}
          key="basic-demo-form"
          formLayout={1}
        >
          <DataForm.Item inputType={"input"} label={"输入框"} name={"input"} />
          <DataForm.Item inputType="number" label="数字框" name="number" />
          <DataForm.Item
            inputType="inputNumberGroup"
            label="数字框组"
            name="numbergroup"
            placeholder={["请输入最小值", "请输入最大值"]}
            required={true}
            rules={[
              {
                min: 100,
                max: 200
              }
            ]}
          />
          <DataForm.Item inputType="textarea" label="文本域" name="textarea" />
          <DataForm.Item inputType="search" label="搜索框" name="search" />
          <DataForm.Item inputType="select" label="下拉框" name="select" options={[
            {
              label: "财务一科",
              value: "1"
            },
            {
              label: "财务二科",
              value: "2"
            }
          ]}/>
          <DataForm.Item inputType="password" label="密码框" name="password" />
          <DataForm.Item
            inputType="cascader"
            label="级联选择"
            name="cascader"
            options={[
              {
                label: '北京',
                value: 'bj',
                children: [
                  {
                    label: '海淀',
                    value: 'hd',
                    children: [
                      {
                        label: '用友',
                        value: 'yy'
                      },
                      {
                        label: '字节',
                        value: 'zj'
                      }
                    ]
                  },
                  {
                    label: '昌平',
                    value: 'cp'
                  }
                ]
              },
              {
                label: '天津',
                value: 'tj',
                children: [
                  {
                    label: '塘沽',
                    value: 'tg'
                  }
                ]
              }
            ]}
          />
          <DataForm.Item inputType="date" label="日期选择" name="date" />
          <DataForm.Item inputType="time" label="时间选择" name="time" />
          <DataForm.Item
            inputType="rangepicker"
            label="日期范围"
            name="range"
          />
          <DataForm.Item inputType="switch" label="开关" name="switch" />
          <DataForm.Item
            inputType="checkboxgroup"
            label="复选框组"
            name="check"
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
            inputType="treeselect"
            label="树选择"
            name="treeselect"
            treeData={[
              {
                title: "Node1",
                value: "0-0",
                key: "0-0",
                children: [
                  {
                    title: "Child Node1",
                    value: "0-0-1",
                    key: "0-0-1"
                  },
                  {
                    title: "Child Node2",
                    value: "0-0-2",
                    key: "0-0-2"
                  }
                ]
              },
              {
                title: "Node2",
                value: "0-1",
                key: "0-1"
              }
            ]}
          />
          <DataForm.Item
            inputType="buttongroup"
            label="按钮组"
            name="buttongroup"
            options={[
              { label: "全部", value: 0 },
              { label: "选择1", value: 1 },
              { label: "选择2", value: 2 },
              { label: "选择3", value: 3 },
              { label: "选择4", value: 4 },
              { label: "选择5", value: 5 }
            ]}
          />
          <DataForm.Item
            inputType="radiogroup"
            label="单选框组"
            name="radio"
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
            inputType="imageupload"
            label="图片上传"
            name="imageupload"
            action="/upload.do"
          />
        </DataForm>
      </div>
    </>
  );
};
export default BasicDemo;
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
