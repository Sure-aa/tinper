---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 表单嵌套、分组
继承于TinperNext-Form组件

```js
import {
  Button,
  Collapse,
  Space
} from "@tinper/next-ui";
import React, { useRef } from "react";
import { DataForm } from "tne-tinpernextpro-fe";
import './demo.less';

const { Panel } = Collapse;

const NestDemo = () => {
  const formRef = useRef(null);

  const onValuesChange = (props, changed) => {
    console.log("FormValueChange-->", props, changed);
    const { type } = props
    if (type) { // 模拟场景切换
      formRef.current.setFieldsValue({
        name: type === 'TENANT_GROUP_GRAY' ? '嘿嘿嘿' : '哈哈哈'
      })
    }
  };
  const onFieldsChange = (props, changed) => {
    console.log("FieldsChange-->", props, changed);
  };
  const getFieldsValue = () => {
    console.log('getFieldsValue \n', formRef.current.validateFields());
  };

  return (
    <>
      <Space className={"demo-wrap--list--buttons"}></Space>
      <div
        className={"demo5-wrapper"}
        style={{
          width: "100%"
        }}
      >
        <DataForm
          ref={formRef}
          onValuesChange={onValuesChange}
          onFieldsChange={onFieldsChange}
          key="basic-demo-form"
          formLayout={3}
          disabledKeys={['approver']}
          hiddenKeys={['advice']}
          invisibleKeys={['date']}
          initialValues={{
            type: "TENANT_GROUP_GRAY",
            name: 'lxy-test',
            des: '💯',
            isolateCode: "a",
            approver: "超级玛丽",
            date: "2019-09-09 12:34:56",
            advice: '快乐，啪，回来了'
          }}
        >
          <Collapse ghost={false} type='list' >
            <Panel header="基本信息" key="basicInfo" showArrow defaultExpanded>
              <DataForm.Item
                inputType="radiogroup"
                label="场景类型"
                name="type"
                required

                options={[
                  {
                    label: "租户组灰度",
                    value: "TENANT_GROUP_GRAY"
                  },
                  {
                    label: "集成隔离",
                    value: "TENATE_ISOLATION"
                  }
                ]}
              />
              <DataForm.Item inputType="input" label="场景名称测试" name="name" required />
              <DataForm.Item inputType="input" label="分流场景简介" name="des" tooltip='天线宝宝' required />
              <DataForm.Item inputType="select" label="维度" name="isolateCode"
                required
                options={[
                  {
                    label: "测试维度a",
                    value: "a"
                  },
                  {
                    label: "测试维度b",
                    value: "b"
                  }
                ]}/>
            </Panel>

            <Panel header="工作流配置" key="workflowConfig" showArrow defaultExpanded>
              <DataForm.Item inputType="input" label="审批人" name="approver" required />
              <DataForm.Item inputType="date" label="审批时间" name="date" required showTime />
              <DataForm.Item inputType="textarea" label="审批意见" name="advice" />
            </Panel>

          </Collapse>
        </DataForm>

        <Button type='primary' onClick={getFieldsValue}>提交</Button>
      </div>
    </>
  );
};

export default NestDemo;
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
