---
tags:
  - TinperNext
  - radio组件
---
# 单选 Radio

## Radio.Group maxCount 展开模式

当maxCount 为true时 需要外层dom 设置一个宽度

```tsx
import { Radio, RadioGroupProps, DatePicker } from '@tinper/next-ui'
import React, { useEffect, useState } from 'react'
import moment from 'moment'

const {RangePicker} = DatePicker
const opts = [
    { label: '今天', value: 'today' },
    { label: '昨天', value: 'yesterday' },
    { label: '近7天', value: 'l7d' },
    { label: '近30天', value: 'l30d' },
    { label: '近90天', value: 'l90d' },
    { label: '本周', value: 'currentWeek' },
    { label: '本月', value: 'currentMonth' },
    { label: '本季', value: 'currentQuarter' },
    { label: '本年', value: 'currentYear' },
];
const btns = [
    <Radio.Button key="1" color="primary" value="1">今天</Radio.Button>,
    <Radio.Button key="2" color="success" value="2">昨天</Radio.Button>,
    <Radio.Button key="3" color="info" value="3">近7天</Radio.Button>,
    <Radio.Button key="4" color="warning" value="4">近30天</Radio.Button>,
    <Radio.Button key="5" color="danger" value="5">近90天</Radio.Button>,
    <Radio.Button key="6" color="dark" value="6">本周</Radio.Button>,
    <Radio.Button key="7" color="dark" value="7">本月</Radio.Button>,
    <Radio.Button key="8" color="dark" value="8">本季</Radio.Button>,
    <Radio.Button key="9" color="dark" value="9">本年</Radio.Button>,
]
const Demo12: React.FC = () => {
    const [selectedValue, setSelectedValue] = useState<RadioGroupProps["value"]>('yesterday');
    const [selectedValue1, setSelectedValue1] = useState<RadioGroupProps["value"]>('2');
    const [pickerValue, setPickerValue] = useState<any>();
    const [pickerValue1, setPickerValue1] = useState<any>();

    useEffect(() => {
        pickerChange()
    }, [])

    useEffect(() => {
        pickerChange('opts')
    }, [selectedValue])

    useEffect(() => {
        pickerChange('btns')
    }, [selectedValue1])

    const handleChange: RadioGroupProps["onChange"] = (value, _event, _option) => {
        setSelectedValue(value as RadioGroupProps["value"]);
    };

    const handleChange1: RadioGroupProps['onChange'] = (value, _e, _option) => {
        setSelectedValue1(value as Required<RadioGroupProps>['value']);
    }
    const timeRangeMappers = {
        'today': () => [moment().startOf('day'), moment().endOf('day')],
        'yesterday': () => [moment().subtract(1, 'days').startOf('day'), moment().subtract(1, 'days').endOf('day')],
        'l7d': () => [moment().subtract(6, 'days').startOf('day'), moment().endOf('day')],
        'l30d': () => [moment().subtract(29, 'days').startOf('day'), moment().endOf('day')],
        'l90d': () => [moment().subtract(89, 'days').startOf('day'), moment().endOf('day')],
        'currentWeek': () => [moment().startOf('week'), moment().endOf('week')],
        'currentMonth': () => [moment().startOf('month'), moment().endOf('month')],
        'currentQuarter': () => [moment().startOf('quarter'), moment().endOf('quarter')],
        'currentYear': () => [moment().startOf('year'), moment().endOf('year')],
        '1': () => [moment().startOf('day'), moment().endOf('day')],
        '2': () => [moment().subtract(1, 'days').startOf('day'), moment().subtract(1, 'days').endOf('day')],
        '3': () => [moment().subtract(6, 'days').startOf('day'), moment().endOf('day')],
        '4': () => [moment().subtract(29, 'days').startOf('day'), moment().endOf('day')],
        '5': () => [moment().subtract(89, 'days').startOf('day'), moment().endOf('day')],
        '6': () => [moment().startOf('week'), moment().endOf('week')],
        '7': () => [moment().startOf('month'), moment().endOf('month')],
        '8': () => [moment().startOf('quarter'), moment().endOf('quarter')],
        '9': () => [moment().startOf('year'), moment().endOf('year')],
    };

    const getTimeRange = (key: any) => {
        return timeRangeMappers[key] ? timeRangeMappers[key]() : null;
    };
    const pickerChange = (flag?: string) => {
        if (flag === 'opts') {
            setPickerValue(getTimeRange(selectedValue))
        } else if (flag === 'btns') {
            setPickerValue1(getTimeRange(selectedValue1))
        }

    }
    return (
        <>
            <div style={{width: '250px'}}>
                <Radio.Group
                    maxCount={true}
                    tiled
                    options={opts}
                    onChange={handleChange}
                    value={selectedValue}
                    optionType="button"
                    showMoreText
                    tiledFooter={<RangePicker
                        allowClear
                        placeholder={['开始日期', '结束日期']}
                        value={pickerValue}
                        onChange={(val: any) => {
                            setSelectedValue('');
                            setPickerValue(val)
                        }}
                    />}
                />
            </div>
            <br/>
            <br/>
            <div style={{width: '280px'}}>
                <Radio.Group
                    name="color"
                    tiled
                    value={selectedValue1}
                    spaceSize='md'
                    size="sm"
                    maxCount={true}
                    showMoreText
                    tiledFooter={<RangePicker
                        allowClear
                        placeholder={['开始日期', '结束日期']}
                        value={pickerValue1}
                        onChange={(val: any) => {
                            setSelectedValue1('');
                            setPickerValue1(val)
                        }}
                    />}
                    onChange={handleChange1}>
                    {btns}
                </Radio.Group>
            </div>

        </>
    );
};

export default Demo12;
```
