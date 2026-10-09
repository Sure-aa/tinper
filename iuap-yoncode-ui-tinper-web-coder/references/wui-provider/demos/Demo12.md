---
tags:
  - TinperNext
  - provider组件
---
# 全局化配置 ConfigProvider

## 全局配置 表单类组件

支持修改组件默认配置

```tsx
import type { ConfigProviderProps } from '@tinper/next-ui';
import {
    AutoComplete,
    Button,
    Cascader,
    Checkbox,
    ColorPicker,
    ConfigProvider,
    DatePicker,
    Form,
    Input,
    InputNumber,
    Pagination,
    Radio,
    Select,
    Space,
    Switch,
    TimePicker,
    TreeSelect
} from '@tinper/next-ui';
import React, { Component } from 'react';

const {TextArea, Password, Search} = Input;
const {Item} = Form;
const {TreeNode} = TreeSelect;

const options = [
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

const defaultOptions = ['jczj', 'dh', 'cd'];

const options1 = [
    {label: 'Apple', value: 'Apple'},
    {label: 'Pear', value: 'Pear'},
    {label: 'Orange', value: 'Orange'},
];

interface ProviderState {
    disabled?: boolean;
    readOnly?: boolean;
    align?: ConfigProviderProps['AlignType'];
    bordered?: ConfigProviderProps['BorderType'];
    browser?: ConfigProviderProps['BrowserType'];
    size?: ConfigProviderProps['SizeType'];
}

class Demo12 extends Component<{}, ProviderState> {
    bRef: Button | null = null;

    constructor(props: {}) {
        super(props);
        this.state = {
            disabled: false,
            readOnly: false,
            align: 'right',
            bordered: 'bottom',
            browser: true,
            size: 'xs'
        };
    }

    handleDisabledChange = (value: boolean) => {
        console.log(value);
        console.log('bRef: disabled--------', this.bRef);
        this.setState({
            disabled: value
        });
    };

    handleReadOnlyChange = (value: boolean) => {
        console.log(value);
        console.log('bRef: readOnly--------', this.bRef);
        this.setState({
            readOnly: value
        });
    };

    handleBorderedChange = (value: ConfigProviderProps['BorderType']) => {
        console.log(value);
        console.log('bRef: bordered--------', this.bRef);
        this.setState({
            bordered: value
        });
    };

    handleAlignChange = (value: ConfigProviderProps['AlignType']) => {
        console.log(value);
        console.log('bRef: align------', this.bRef);
        this.setState({
            align: value
        });
    };

    handleBrowserChange = (value: ConfigProviderProps['BrowserType']) => {
        console.log(value);
        console.log('bRef: browser------', this.bRef);
        this.setState({
            browser: value
        });
    };

    handleSizeChange = (value: ConfigProviderProps['SizeType']) => {
        console.log(value);
        this.setState({
            size: value
        });
    };

    render() {
        const {bordered, readOnly, align, disabled, browser, size} = this.state;
        return (
            <div className='demo12'>
                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group
                        style={{marginRight: 20}}
                        selectedValue={readOnly}
                        className='custom-readOnly'
                        onChange={this.handleReadOnlyChange}
                    >
                        <Radio.Button value={true}>只读</Radio.Button>
                        <Radio.Button value={false}>非只读</Radio.Button>
                    </Radio.Group>
                </div>

                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group
                        style={{marginRight: 20}}
                        selectedValue={disabled}
                        className='custom-disbled'
                        onChange={this.handleDisabledChange}
                    >
                        <Radio.Button value={true}>禁用</Radio.Button>
                        <Radio.Button value={false}>不禁用</Radio.Button>
                    </Radio.Group>
                </div>

                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group
                        style={{marginRight: 20}}
                        selectedValue={bordered}
                        className='custom-border'
                        onChange={this.handleBorderedChange}
                    >
                        <Radio.Button value='bottom'>下划线</Radio.Button>
                        <Radio.Button value={undefined}>默认</Radio.Button>
                        <Radio.Button value={false}>无边框</Radio.Button>
                    </Radio.Group>
                </div>

                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group style={{marginRight: 20}} selectedValue={align} onChange={this.handleAlignChange}>
                        <Radio.Button value='left'>左对齐</Radio.Button>
                        <Radio.Button value='center'>居中</Radio.Button>
                        <Radio.Button value='right'>右对齐</Radio.Button>
                        <Radio.Button value={undefined}>默认</Radio.Button>
                    </Radio.Group>
                </div>

                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group style={{marginRight: 20}} selectedValue={browser} onChange={this.handleBrowserChange}>
                        <Radio.Button value={true}>浏览态</Radio.Button>
                        <Radio.Button value={false}>非浏览态</Radio.Button>
                        <Radio.Button value={undefined}>默认</Radio.Button>
                    </Radio.Group>
                </div>

                <div style={{display: 'flex', alignItems: 'center', marginBottom: 20}}>
                    <Radio.Group style={{marginRight: 20}} selectedValue={size} onChange={this.handleSizeChange}>
                        <Radio.Button value={'xs'}>xs</Radio.Button>
                        <Radio.Button value={'sm'}>sm</Radio.Button>
                        <Radio.Button value={'md'}>md</Radio.Button>
                        <Radio.Button value={'nm'}>nm</Radio.Button>
                        <Radio.Button value={'lg'}>lg</Radio.Button>
                        <Radio.Button value={undefined}>默认</Radio.Button>
                    </Radio.Group>
                </div>

                <ConfigProvider disabled={disabled} bordered={bordered} align={align} browser={browser} size={size} readOnly={readOnly}>
                    <Space style={{width: '100%'}} direction='vertical'>
                        <ConfigProvider>
                            <Form>
                                <Item label='自动填充'>
                                    <AutoComplete
                                        style={{width: '200px'}}
                                        value='1'
                                        options={['10000', '10001', '10002', '11000', '12010']}
                                    />
                                </Item>
                                <Item label='取色器'>
                                    <ColorPicker value='#f00' />
                                </Item>
                                <Item label='级联菜单' required>
                                    <Cascader placeholder='请选择' defaultValue={defaultOptions} options={options} />
                                </Item>
                                <Item label='下拉框'>
                                    <Select value={123} style={{width: '200px'}}></Select>
                                </Item>
                                <Item label='日期'>
                                    <DatePicker value='2023-03-03' />
                                </Item>
                                <Item label='日期范围'>
                                    <DatePicker picker='range' value={['2023-03-03', '2023-08-08']} />
                                </Item>
                                <Item label='时间输入框'>
                                    <TimePicker value='11:11:11' />
                                </Item>
                                <Item label='输入框'>
                                    <Input value='十里春风' />
                                </Item>
                                <Item label='搜索框'>
                                    <Search value='众里寻她' />
                                </Item>
                                <Item label='搜索框(确认按钮)'>
                                    <Search value='千百度' enterButton='搜索' />
                                </Item>
                                <Item label='密码框'>
                                    <Password value='你猜啊' />
                                </Item>
                                <Item label='数字输入框'>
                                    <InputNumber value={666} />
                                </Item>
                                <Item label='文本输入框'>
                                    <TextArea value={'两次经济大危机的比较研究'} style={{width: '300px'}} />
                                </Item>
                                <Item label='树选择' required>
                                    <TreeSelect
                                        allowClear
                                        treeNodeLabelProp='value'
                                        style={{width: '200px'}}
                                        placeholder='请选择'
                                    >
                                        <TreeNode value='parent 1' title='用友网络股份有限公司' key='0-1'>
                                            <TreeNode value='parent 1-0' title='用友网络股份有限公司1-0' key='0-1-1'>
                                                <TreeNode value='leaf1' title='用友网络股份有限公司leaf' key='random' />
                                                <TreeNode
                                                    value='leaf2'
                                                    title='用友网络股份有限公司leaf'
                                                    key='random1'
                                                />
                                                <TreeNode
                                                    value='leaf3'
                                                    title='用友网络股份有限公司leaf'
                                                    key='random32'
                                                />
                                                <TreeNode
                                                    value='leaf4'
                                                    title='用友网络股份有限公司leaf'
                                                    key='random33'
                                                />
                                                <TreeNode
                                                    value='leaf5'
                                                    title='用友网络股份有限公司leaf'
                                                    key='random4'
                                                />
                                                <TreeNode
                                                    value='leaf6'
                                                    title='用友网络股份有限公司leaf'
                                                    key='random5'
                                                />
                                            </TreeNode>
                                            <TreeNode value='parent 1-1' title='用友网络股份有限公司' key='random2'>
                                                <TreeNode value='sss' title='用友网络股份有限公司' key='random3' />
                                            </TreeNode>
                                        </TreeNode>
                                    </TreeSelect>
                                </Item>
                                <Item label='单选'>
                                    <Radio.Group name="fruits" value={'1'}>
                                        <Radio value="1" inverse>苹果</Radio>
                                        <Radio value="2" inverse>香蕉</Radio>
                                        <Radio value="3" inverse>葡萄</Radio>
                                    </Radio.Group>
                                </Item>
                                <Item label='多选'>
                                    <Checkbox.Group options={options1} value={['Apple', 'Pear']} />
                                </Item>
                                <Item label='开关'>
                                    <Switch />
                                </Item>
                            </Form>
                            {browser ? null : <Pagination
                                prev
                                next
                                maxButtons={5}
                                boundaryLinks
                                defaultActivePage={2}
                                defaultPageSize={15}
                                showJump={true}
                                total={50}
                            />}
                        </ConfigProvider>
                    </Space>
                </ConfigProvider>

                <Button type='primary' ref={ref => (this.bRef = ref)}>
                    按钮
                </Button>
            </div>
        );
    }
}

export default Demo12;
```
