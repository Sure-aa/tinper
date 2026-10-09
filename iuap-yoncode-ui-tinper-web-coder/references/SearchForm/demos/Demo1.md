---
tags:
  - TinperNextPro
  - SearchForm组件
---
# SearchForm 查询表单

## 基础查询表单
继承于TinperNext-Form组件。支持labelWidth 自定义label 宽度

```js
import React, { useRef } from "react";
import { SearchForm } from "tne-tinpernextpro-fe";
import { Select, Space, Radio, ConfigProvider } from "@tinper/next-ui";

const Option = Select.Option;

const cascaderOptions = [
  {
    label: '基础组件',
    value: 'jczj',
    children: [
      {
        label: '导航',
        value: 'dh',
        children: [
          {
            label: '面包屑',
            value: 'mbx'
          },
          {
            label: '分页',
            value: 'fy'
          },
          {
            label: '标签',
            value: 'bq'
          },
          {
            label: '菜单',
            value: 'cd'
          }
        ]
      },
      {
        label: '反馈',
        value: 'fk',
        children: [
          {
            label: '模态框',
            value: 'mtk'
          },
          {
            label: '通知',
            value: 'tz'
          }
        ]
      },
      {
        label: '表单',
        value: 'bd'
      }
    ]
  },
  {
    label: '应用组件',
    value: 'yyzj',
    children: [
      {
        label: '参照',
        value: 'ref',
        children: [
          {
            label: '树参照',
            value: 'reftree'
          },
          {
            label: '表参照',
            value: 'reftable'
          },
          {
            label: '穿梭参照',
            value: 'reftransfer'
          }
        ]
      }
    ]
  }
];

const selectOptions = [
  { label: '按方法结算', describe: '通过专项成本方法计算转出成本金额', value: '1' },
  { label: '按内容结算', describe: '通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额成本金，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额，通过维护成本转出要素范围及比例等根据实际投入成本计算转出成本金额成本金', value: '2' },
  { label: '按明细结算', describe: '根据实际投入成本明细维护转出成本金额', value: '3' }
]

const BasicDemo = () => {
  const formRef = useRef(null);
  const [locale, setLocale] = React.useState('zh-cn');
  const [dir, setDir] = React.useState('ltr');
  const onValuesChange = (values, allValues) => {
    console.log('onValuesChange', values, allValues);
  }

  // useEffect(() => {
  //   formRef.current?.setFieldsValue({
  //     select: 'zhangsan',
  //     input: '小花狗不见了',
  //     numbergroup: [102, 103]
  //   })
  // }, [])

  return (
    <>
      <Space className={"demo-wrap--list--buttons"}>
        多语设置:
        <Radio.Group value={locale} onChange={value => setLocale(value)}>
          <Radio value="zh-cn" inverse>中文</Radio>
          <Radio value="en-us" inverse>英语</Radio>
        </Radio.Group>
      </Space>
      <div
        style={{
          width: "100%"
        }}
      >
        <ConfigProvider locale={locale} dir={dir} layout={locale === 'zh-cn' ? "horizontal" : "vertical"}>
          <SearchForm
            ref={formRef}
            onValuesChange={onValuesChange}
            onCollapse={(collapsed) => { console.log('onCollapse', collapsed) } }
            key="basic-search-form"
            size="sm"
            onSearch={(values, errors, obj) => { console.log('onSearch', obj) }}
            onReset={(values, formIns) => { console.log('onReset', values, formIns) }}
            initialValues={{ select: 'zhangsan', input: '小花狗不见了', numbergroup: [102, 103], switch: false }}
            showSelected={true}
            instant={true}
          >
            <SearchForm.Item inputType={"input"} label={"输入框"} name={"input"} required />
            <SearchForm.Item inputType="number" label="数字框" name="number" />
            <SearchForm.Item
              hidden={true}
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
            <SearchForm.Item inputType="search" label="搜索框" name="search" />
            <SearchForm.Item mode="multiple" inputType="select" label="下拉框" name="select"
              options={[
                {
                  key: "zhangsan",
                  label: "张三",
                  value: "zhangsan",
                  id: "zhangsan"
                },
                {
                  key: "lisi",
                  label: "李四",
                  value: "lisi",
                  id: "lisi"
                },
                {
                  key: "wangwu",
                  label: "王五",
                  value: "wangwu",
                  id: "wangwu"
                }
              ]}
            />
            <SearchForm.Item inputType="password" label="密码框" name="password" />
            <SearchForm.Item
              inputType="cascader"
              label="级联选择"
              name="cascader"
              options={cascaderOptions}
            />
            <SearchForm.Item inputType="date" label="日期选择" name="date" />
            <SearchForm.Item inputType="time" label="时间选择" name="time" />
            <SearchForm.Item
              inputType="rangepicker"
              label="日期范围"
              name="range"
              format="MM-DD-YYYY"
            />
            <SearchForm.Item inputType="switch" label="开关" name="switch" />
            <SearchForm.Item
              inputType="checkboxgroup"
              optionType="button"
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
                },
                {
                  label: "选项4",
                  value: "4"
                },
                {
                  label: "选项5",
                  value: "5"
                },
                {
                  label: "选项6",
                  value: "6"
                }
              ]}
            />
            <SearchForm.Item
              inputType="treeselect"
              label="树选择"
              name="treeselect"
              multiple
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
            <SearchForm.Item
              inputType="radiogroup"
              label="按钮组"
              name="buttongroup"
              optionType="button"
              spaceSize="md"
              onChange={(value, info) => console.log('onChange', info.currentTarget)}
              options={[
                { label: "全部", value: 0 },
                { label: "选择1", value: 1 },
                { label: "选择2", value: 2 },
                { label: "选择3", value: 3 },
                { label: "选择4", value: 4 },
                { label: "选择5", value: 5 }
              ]}
            />
            <SearchForm.Item
              inputType="custom"
              label="自定义select"
              name="custom_select"
            >
              <Select mode="multiple" optionLabelProp='key'>
                {
                  selectOptions.map(item => {
                    return (
                      <Option key={item.label} label={item.label} value={item.value}>
                        <h3>{item.label}</h3>
                        <span>{item.describe}</span>
                      </Option>
                    )
                  })
                }
              </Select>
            </SearchForm.Item>
          </SearchForm>
        </ConfigProvider>
      </div>
    </>
  );
};
export default BasicDemo;
```
