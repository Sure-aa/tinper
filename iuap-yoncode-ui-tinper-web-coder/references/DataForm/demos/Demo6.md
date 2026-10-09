---
tags:
  - TinperNextPro
  - DataForm组件
---
# DataForm 数据表单

## 表单浏览态
支持表单浏览态，可自定义预览态渲染函数 previewRender

```js
import { Button, Collapse, Rate, Space } from "@tinper/next-ui";
import moment from "moment";
import React, { useRef, useState } from "react";
import { DataForm } from "tne-tinpernextpro-fe";
import { china } from "./china";
import "./demo.less";

const { Panel } = Collapse;

const treeData = [
  {
    title: "河北",
    value: "hebei",
    key: "hebei",
    children: [
      {
        title: "秦皇岛",
        value: "qinhuangdao",
        key: "qinhuangdao"
      },
      {
        title: "北戴河",
        value: "beidaihe",
        key: "beidaihe"
      }
    ]
  },
  {
    title: "北京",
    value: "beijing",
    key: "beijing"
  }
];

const NestDemo = () => {
  const formRef = useRef(null);
  const [formMode, setFormMode] = useState("edit");
  const [rate, setRate] = useState(1);
  const [required, setRequired] = useState(false);
  const [bordered, setBordered] = useState();

  const initValues = {
    input: "lxy-test",
    inputsuffix: "💯",
    search: "search text",
    cascader: ["46", "4604", "460400111"],
    cascadermultiple: [
      ["11", "1101", "110105"],
      ["21", "2113"]
    ],
    radiogroup: "TENANT_GROUP_GRAY",
    checkboxgroup: ["js", "python"],
    radiogroup: false,
    password: "123456",
    switch: true,
    number: 1234567,
    inputNumberGroup: [18, 150],
    time: moment("23:59:59", "HH:mm:ss"),
    rangepicker: ["08月01日2024年", "09月11日2025年"],
    rangepickerquarter: ["2020-Q1", "2025-Q4"],
    selectmultiple: ["joker", "cute"],
    // selectmultiple: 'joker',
    treeselectsingle: "beidaihe",
    treeselectmulitiple: ["beidaihe", "beijing"],
    select: "xinba",
    date: moment("07/29/2024 13:34:56"),
    textarea: "快乐，啪，回来了",
    custom: rate
  };

  // const [values, setValues] = useState(initValues)

  const handleChangeRate = value => {
    setRate(value);
  };

  const previewRenderCustom = ({ name, value, props }) => {
    let level = "";
    if (value === 5) {
      level = "大满贯";
    } else if (value >= 4.5) {
      level = "优秀";
    } else if (value >= 4) {
      level = "良好";
    } else if (value >= 3) {
      level = "及格";
    } else {
      level = "恭喜你，未来可期";
    }
    return level;
  };

  const onValuesChange = (props, changed) => {
    console.log("FormValueChange-->", props, changed);
    const { radiogroup } = props;
    if (radiogroup) {
      // 模拟场景切换
      formRef.current.setFieldsValue({
        input: radiogroup === "TENANT_GROUP_GRAY" ? "嘿嘿嘿" : "哈哈哈"
      });
    }
  };
  const onFieldsChange = (props, changed) => {
    console.log("FieldsChange-->", props, changed);
  };

  // 切换模式时，需传入数据源 values 或 setFieldsValue
  const changeFormMode = () => {
    // const currentValues = formRef.current.getFieldsValue()
    // console.log('111-------changeFormMode', currentValues);
    // setValues(currentValues)
    if (formMode === "edit") {
      formRef.current.setFieldsValue({
        input: "堂下何人，竟敢状告本官！",
        number: 1234567
      });
    }
    setFormMode(formMode === "browse" ? "edit" : "browse");
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
          key='basic-demo-form'
          formLayout={3}
          bordered={bordered}
          disabledKeys={['search']}
          // hiddenKeys={['textarea']}
          // invisibleKeys={['date']}
          initialValues={initValues}
          // values={{ ...values, textarea: '那厮乃混元一气上方太乙金仙美猴王齐天大圣斗战胜佛孙悟空' }}
          formMode={formMode}
        >
          <Collapse ghost={false} type='list'>
            <Panel header='基本信息' key='basicInfo' showArrow defaultExpanded>
              <DataForm.Item inputType='input' label='场景名称测试' name='input' required={required} />
              <DataForm.Item
                inputType='input'
                label='分流场景简介'
                name='inputsuffix'
                tooltip='天线宝宝'
                suffix={"%"}
                fieldid='input_fieldid'
                required={required}
                // pattern={/^[a-zA-Z0-9]+$/}
                // patternMsg='格式错误'
                rules={[
                  // {
                  //   pattern: /^[a-zA-Z0-9]+$/,
                  //   message: '用户名格式错误'
                  // },
                  {
                    validator (rules, value) {
                      // console.log('111------inputsuffix', rules, value);
                      return new Promise((resolve, reject) => {
                        if (value === "lxy") {
                          reject(Error("应是天仙狂醉，乱把白云揉碎"));
                        } else {
                          resolve();
                        }
                      });
                    }
                  }
                ]}
              />
              <DataForm.Item inputType='search' label='搜索框' name='search' required={required} />

              <DataForm.Item
                inputType='cascader'
                label='所属地区'
                name='cascader'
                required={required}
                options={china}
                tooltip='数据源非最新,如儋州数据已更新'
                fieldNames={{ label: "name", value: "code", children: "children" }}
                separator=' > '
                fieldid='cascader_fieldid'
              />
              <DataForm.Item
                required={required}
                inputType='cascader'
                label='所属地区(多选)'
                name='cascadermultiple'
                options={china}
                fieldNames={{ label: "name", value: "code", children: "children" }}
                multiple
                maxTagCount={2}
                maxTagTextLength={3}
              />

              <DataForm.Item
                required={required}
                inputType='radiogroup'
                label='场景类型'
                name='radiogroup'
                optionType='button'
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
              <DataForm.Item
                required={required}
                inputType='checkboxgroup'
                label='支持文件类型'
                name='checkboxgroup'
                options={[
                  {
                    label: "JS",
                    value: "js"
                  },
                  {
                    label: "JAVA",
                    value: "java"
                  },
                  {
                    label: "Python",
                    value: "python"
                  }
                ]}
              />
              <DataForm.Item
                required={required}
                inputType='radiogroup'
                label='你喜欢的水果ffffgggggggggggggggggggggggg'
                name='radiogroup'
                options={[
                  {
                    label: "莲雾",
                    value: true
                  },
                  {
                    label: "鸡蛋果",
                    value: false
                  }
                ]}
              />
              <DataForm.Item required={required} inputType='password' label='密码' name='password' />
              <DataForm.Item
                required={required}
                inputType='number'
                label='项目金额'
                name='number'
                addonBefore={"$"}
                showMark
                toThousands
              />
              <DataForm.Item
                required={required}
                inputType='inputNumberGroup'
                label='数字区间'
                name='inputNumberGroup'
              />
              <DataForm.Item
                required={required}
                inputType='time'
                label='截止时间'
                name='time'
                showSecond={false}
                use12Hours
              />
              <DataForm.Item
                required={required}
                inputType='rangepicker'
                label='日期范围'
                name='rangepicker'
                format='MM月DD日YYYY年'
              />
              <DataForm.Item
                required={required}
                inputType='rangepicker'
                label='季度范围'
                name='rangepickerquarter'
                picker='quarter'
                separator='至'
              />

              <DataForm.Item
                required={required}
                inputType='select'
                label='维度'
                name='selectmultiple'
                mode='multiple'
                // multiple
                fieldNames={{ label: "name", value: "id", children: "options" }}
                options={[
                  {
                    name: "人类",
                    id: "human",
                    options: [
                      {
                        key: "boy",
                        name: "唐三",
                        id: "joker"
                      },
                      {
                        key: "girl",
                        name: "小舞",
                        id: "princess"
                      }
                    ]
                  },
                  {
                    name: "精灵",
                    id: "🧚",
                    options: [
                      {
                        key: "monkey",
                        name: "毛球",
                        id: "cute"
                      }
                    ]
                  }
                ]}
              />

              <DataForm.Item
                required={required}
                inputType='treeselect'
                label='树选择'
                name='treeselectsingle'
                treeData={treeData}
              />

              <DataForm.Item
                required={required}
                inputType='treeselect'
                label='树选择(多选)'
                name='treeselectmulitiple'
                treeData={treeData}
                multiple
              />
              <DataForm.Item required={required} inputType='colorpicker' label='选择颜色' name='colorpicker' />
            </Panel>

            <Panel header='工作流配置' key='workflowConfig' showArrow defaultExpanded>
              <DataForm.Item
                required={required}
                inputType='select'
                label='审批人'
                name='select'
                options={[
                  {
                    label: "狮子王",
                    value: "shiziwang"
                  },
                  {
                    label: "辛巴",
                    value: "xinba"
                  }
                ]}
              />
              <DataForm.Item required={required} inputType='switch' label='是否通过' name='switch' />
              <DataForm.Item
                required={required}
                inputType='date'
                label='审批时间'
                name='date'
                showTime
                use12Hours
                format='MM/DD/YYYY hh:mm:ss a'
              />
              <DataForm.Item required={required} inputType='textarea' label='审批意见' name='textarea' autoSize={{ minRows: 3, maxRows: 5 }} />
              <DataForm.Item
                required={required}
                inputType='custom'
                label='自定义组件'
                name='custom'
                previewRender={previewRenderCustom}
                fieldid='custom_fieldid'
              >
                <Rate autoFocus allowHalf value={rate} onChange={handleChangeRate} />
              </DataForm.Item>
            </Panel>
          </Collapse>
        </DataForm>

        <Button style={{ marginLeft: 20 }} onClick={() => setRequired(!required)}>切换必填</Button>

        <Button style={{ marginLeft: 20 }} onClick={() => setBordered(bordered === 'bottom' ? undefined : 'bottom')}>切换下划线模式</Button>

        <Button type='info' style={{ marginLeft: 20 }} onClick={changeFormMode}>
          {formMode === "edit" ? "预览" : "编辑"}
        </Button>

        <Button htmlType='submit' type='danger' style={{ marginLeft: 20 }}>校验</Button>
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
