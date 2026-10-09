---
tags:
  - TinperNextPro
  - EditTable组件
---
# EditTable 编辑表格

## 行内编辑方式以及行联动
继承于TinperNext-Table组件。

```js
import { Button, Switch, Space , ConfigProvider, Modal} from "@tinper/next-ui";
import React, { useMemo, useRef, useState, useCallback, useEffect } from "react";
import { EditTable } from 'tne-tinpernextpro-fe';

const data = [
  {
    id: "1", a: "yonyou_2", b: "北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市北京市", age: 18, adds: ["北京", "海淀", "用友"], newAdds: 'bj', oldAdds: ["bj", "cd"], c: "男", d: "财务一科", e: ["T1"], g: false, h: '2021-04-23', i: '10:00', j: 'XXXXX', k: "bip", key: "2",
    children: [
      { id: "1-1", a: "yonyou_-1", b: "昌平区", age: 18, adds: ["北京", "海淀", "用友"], newAdds: 'bj', oldAdds: ["bj", "cd"], c: "男", d: "财务一科", e: ["T1"], g: false, h: '2021-04-23', i: '10:00', j: 'XXXXX', k: "bip", key: "101" }
    ]
  },
  { id: "2", a: "yonyou_3", b: "上海市", age: 18, adds: ["北京", "海淀", "用友"], newAdds: 'bj', oldAdds: ['tj'], c: "女", d: "财务一科", e: ["T2"], g: true, h: '2022-04-23', i: '10:00', j: 'XXXXX', k: "bip", key: "3" },
  { id: "3", a: "yonyou_4", b: "深圳市", age: 18, adds: ["北京", "海淀", "用友"], newAdds: 'bj', oldAdds: ["bj", "tj", "cd"], c: "男", d: "财务一科", e: ["T1"], g: false, h: '2021-04-23', i: '10:00', j: 'XXXXX', k: "bip", key: "4" }

];

// ['bj', 'hd', 'yy']
const EditTableDemo = (props) => {
  const ref = useRef()

  const [isEditKeys, setIsEditKeys] = useState([])
  const [expandedRowKeys, setExpandedRowKeys] = useState([]);
  const [selectedRowKeys, setSelectedRowKeys] = useState([])

  const columns = useMemo(() => {
    return [
      {
        title: "性别",
        dataIndex: "c",
        key: "c",
        width: 100,
        editType: 'select',


        // render: (text, record, index, { column }) => {
        //   const arr = column.editOptions.options;
        //   return text + 'ss'
        // },
        editOptions: {
          defaultValue: "1",
          options: [
            {
              label: "男",
              value: "1"
            },
            {
              label: "女",
              value: "2"
            }
          ]
        },
        onCellChange: (record, col, val) => {
          ref.current.saveMultiCellData({ rowData: { ...record, [col.key]: val, d: "2" } });
        }
      },
      {
        title: "treeselect",
        dataIndex: "treeselect",
        key: "treeselect",
        width: 100,
        editType: 'treeselect',
        showEllipsisTitle:false,
        render: (text, record, index, { column }) => {
          const arr = column.editOptions.options;
          return text
        },
        editOptions: {
          // getPopupContainer: () => document.querySelector('.editTableModal'),
          // multiple:true,
          defaultValue: "1",
          treeData: [
              { title: 'pNode 01', value: '0-0', key: '0-0', disabled: true ,
                 children: [{
                    title: 'Child Node1',
                    value: '0-0-1',
                    key: '0-0-1',
                }, 
                {
                    title: 'Child Node2',
                    value: '0-0-2',
                    key: '0-0-2',
                }],
              },
                { title: 'pNode 011', value: '0-0', key: '0-3', disabled: true ,
                 children: [{
                    title: 'Child Node1',
                    value: '0-0-1',
                    key: '0-0-1',
                }, 
                {
                    title: 'Child Node2',
                    value: '0-0-2',
                    key: '0-0-2',
                }],
              },
            { title: 'pNode 02', value: '0-1', key: '0-1' },
            { title: 'pNode 03', value: '0-2', key: '0-2', isLeaf: true },
          ]
        },
        onCellChange: (record, col, val) => {
          ref.current.saveMultiCellData({ rowData: { ...record, [col.key]: val, d: "2" } });
        }
      },
      {
        title: "行按钮键值",
        dataIndex: "key",
        key: "key",
        width: 250,
        hidden: true,
        editType: 'input',
        editOptions: {
          placeholder: '请输入员工编号',
          type: 'textarea'
        },
        formItemProps: {},
        children: [],
        onCellChange: (record, col, val) => {
          // ref.current.saveMultiCellData({ rowData: { ...record, [col.key]: val, a: String(Math.random() * 1000) } });
        }

      },
      {
        title: "员工编号",
        dataIndex: "a",
        key: "a",
        width: 250,
        editType: 'input',
        editOptions: {
          placeholder: '请输入员工编号',
          type: 'textarea'
        },
        children: [],
        onCellChange: () => {}
      },
      {
        title: "员工姓名",
        dataIndex: "b",
        key: "b",
        width: 100,
        children: [],
        editType: 'input',
        editOptions: {
          placeholder: '请设置员工姓名'
        },
        editTip: '编辑提示',
        helpTip: '帮助提示',
        pattern: /^[a-zA-Z0-9\u4e00-\u9fa5][_a-zA-Z0-9\u4e00-\u9fa5]*$/g,
        patternMsg: '仅支持汉字/字母/数字/下划线，不能以下划线开头',
        required: true,
        validateTrigger: 'onChange',
        validator: (value, record, data, callback) => {
          console.log('record', record, 'data', data)
          const reg = /^[a-zA-Z0-9\u4e00-\u9fa5][_a-zA-Z0-9\u4e00-\u9fa5]*$/g;
          if (!reg.test(value)) {
            callback('仅支持汉字/字母/数字/下划线，不能以下划线开头')
          } else if (value && value.length > 6) {
            callback('不能超过6个字符')
          } else {
            callback()
          }
        }
      },
      {
        title: "年龄",
        dataIndex: "age",
        key: "age",
        width: 100,
        children: [],
        editType: 'number',
        helpTip: '帮助提示',
        editTip: '编辑提示',
        // editAbled: (record) => {
        //   console.log('record==', record)
        //   return false
        // },
        editOptions: {
          placeholder: '请设置员工年龄',
          min: 0.01,
          // readOnly: "true",
          defaultValue: 18,
          precision: 2
        },
        validator: (value, record, data, callback) => {
          console.log('value', value, 'record', record, 'data', data)
          if (!value) {
            callback('不能为空')
          } else if (value > 20) {
            callback('不能大于20')
          } else if (value < 16) {
            callback('不能小于16')
          } else {
            callback()
          }
        }
      },

      {
        title: "部门",
        dataIndex: "d",
        key: "d",
        width: 100,
        children: [],
        editType: 'select',
        editOptions (record, index, col) {
          return {
            disabled: record.c == "2",
            defaultValue: "1",
            options: [
              {
                label: "财务一科",
                value: "1"
              },
              {
                label: "财务二科",
                value: "2"
              }
            ]
          }
        },
        render: (text, record, index, { column }) => {
          const arr = column.editOptions.options;
          return text
            ? arr.filter((option, index) => {
              return option.value === text
            })[0]?.label
            : "--"
        }
      },
      {
        title: "职级",
        dataIndex: "e",
        key: "e",
        width: 100,
        children: [],
        editType: 'select',
        render: (text, record, index, { column }) => {
          const arr = column.editOptions.options;
          return text
            ? text.map((item, index) => {
              const itemFiltered = arr.filter(option => option.value === item)[0];
              return itemFiltered ? itemFiltered.label : item;
            }).join(",")
            : "--"
        },
        editOptions: {
          mode: "tags",
          separator: ",",
          options: [
            {
              label: "高级",
              value: "T1"
            },
            {
              label: "中级",
              value: "T2"
            },
            {
              label: "初级",
              value: "T3"
            }
          ]
        }
      },
      {
        title: "在职",
        dataIndex: "g",
        key: "g",
        width: 100,
        children: [],
        editType: 'switch',
        editOptions: {}
      },
      {
        title: "入职日期",
        dataIndex: "h",
        key: "h",
        width: 200,
        children: [],
        editType: 'date',
        editOptions: {
          placeholder: '请选择日期'
        }
      },
      {
        title: "住址",
        dataIndex: "adds",
        key: "adds",
        width: 200,
        children: [],
        editType: 'cascader',
        render: (text) => {
          return text ? text.join() : "-";
        },
        // textToFormItemValue: (text) => {
        //   return text ? text.split(',') :[]
        // },
        editOptions: {
          placeholder: '请选择住址',
          options: [
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
          ]
        }
      },
      {
        title: "现住地址",
        dataIndex: "newAdds",
        key: "newAdds",
        width: 200,
        children: [],
        editType: 'radiogroup',
        render: (text, record, index, { column }) => {
          const options = column.editOptions.options;
          return options.filter(item => item.value === text)[0]?.label || "-";
        },
        editOptions: {
          options: [
            { label: '北京', value: 'bj' },
            { label: '天津', value: 'tj' },
            { label: '成都', value: 'cd' }
          ]
        }
      },
      {
        title: "曾住地址",
        dataIndex: "oldAdds",
        key: "oldAdds",
        width: 200,
        children: [],
        editType: 'checkboxgroup',
        render: (text, record, index, { column }) => {
          const options = column.editOptions.options;
          return text
            ? text.map(item => {
              return options.filter(option => option.value === item)[0].label;
            }).join()
            : "-"
        },
        editOptions: {
          options: [
            { label: '北京', value: 'bj' },
            { label: '天津', value: 'tj' },
            { label: '成都', value: 'cd' }
          ]
        }
      },
      {
        title: "入职时间",
        dataIndex: "i",
        key: "i",
        width: 200,
        children: [],
        editType: 'time',
        editOptions: {
          placeholder: '请选择时间'
        }
      },
      {
        title: "入职介绍",
        dataIndex: "j",
        key: "j",
        width: 200,
        children: [],
        editOptions: {

        }
      },
      // {
      //   title: "部门",
      //   dataIndex: "k",
      //   key: "k",
      //   width: 200,
      //   children: [],
      //   editType: 'reftabletree',
      //   editOptions: {
      //     onTreeChange: (value) => {},
      //     page: {
      //       pageCount: 0,
      //       currPageIndex: 0,
      //       totalElements: 17
      //     }
      //   }
      // },
      {
        title: "w",
        dataIndex: "w",
        key: "w",
        width: 200,
        editAbled: false,
        singleFilter: false,
        singleFind: false
      }
    ]
  }, [isEditKeys]);

  const addDataFirst = () => {
    ref.current.addRow({
      callback: ({ isEditKeys }) => {
        console.log('isEditKeys', isEditKeys)
        setIsEditKeys(isEditKeys)
      }
    })
  }

  const addDataLast = () => {
    ref.current.addRowLast({
      callback: (data, isEditKeys) => {
        console.log('isEditKeys', isEditKeys)
        setIsEditKeys(isEditKeys)
      }
    })
  }

  const copyRowDataBatch = () => {
    const rows = ref.current.getSelectedRows();
    const rowData = rows.map(item => {
      return {
        ...item,
        children: [],
        key: Math.random().toString(36).substr(2)
      }
    })
    rowData.length && ref.current.addRow({ rowData })
  }
  const delRowDataBatch = () => {
    const selectedKeys = ref.current.getSelectedRowKeys()
    deleteData({
      rowKey: selectedKeys,
      callback: () => {

      }
    })
  }

  const onPopMenuClick = (options, data, isEditKey) => {
    // let isEditKeys = ref.current?.getIsEditKey()
    console.log('options', options, isEditKey)
    setIsEditKeys(isEditKey)
  }

  const rowSelection = {
    selectedRowKeys,
    // getCheckboxProps: (record) => ({
    //   disabled: record.key == '3',
    //   name: record.b
    // }),
    onChange: (selectedRowKeys, selectedRows) => {
      console.log('selectedRowKeys', selectedRowKeys, 'selectedRows', selectedRows);
      setSelectedRowKeys(selectedRowKeys)
    },
    onSelectAll: (check, selectedRows, changeRows) => {
      console.log('check', check, 'selectedRows', selectedRows, 'changeRows', changeRows);
    }
  };

  const deleteData = (currentKey) => {
    ref.current?.deleteData(currentKey, () => {
      console.log(ref.current?.getDeleteRowKeys())
    })
  }
  const isLastEle = (rowKey, innerData) => {
    if(rowKey === innerData[innerData.length -1 ]?.key) return true;
   
    let curIndex = -1;
    for (let i = 0; i < innerData.length; i++) {
      if(innerData[i].key === rowKey) {
        return i === innerData.length - 1;

      }
      let isLast = false;
      if(innerData[i].children && innerData[i].children.length) {
        isLast = isLastEle(rowKey, innerData[i].children)
      }
      if(isLast) {
        return true
      }

    }


  }
  const isFirstEle = (rowKey, innerData) => {
   
    if(rowKey === innerData[0].key) return true;

    let curIndex = -1;
    for (let i = 0; i < innerData.length; i++) {
      if(innerData[i].key === rowKey) {
        curIndex = i;
        break
      }
      let isFirst = false;
      if(innerData[i].children && innerData[i].children.length) {
        isFirst = isFirstEle(rowKey, innerData[i].children)
      }
      if(isFirst) {
        return true
      }

    }
    if(curIndex === 0) {
      return true
    }


  }



  const operationItems = useCallback((record, index, isEdit, innerOperations, innerData) => {
    console.log(innerData, 'innerData')
    const commonItem = [
      {
        key: 'del',
        text: '删除'
      },
      {
        key: 'child',
        text: '插入子级'
      },
      {
        key: 'copyData',
        text: '复制行'
      },
      {
        key: 'before',
        text: '在上方插入行'
      },
      {
        key: 'after',
        text: '在下方插入行'
      },
      {
        key: 'up',
        text: '上移'
      },
      {
        key: 'down',
        text: '下移'
      }

    ]
    if (isFirstEle(record.key, innerData)) {

      commonItem.splice(5, 1)
    }
    if (isLastEle(record.key, innerData)) {
      commonItem.splice(commonItem.length-1, 1)
    }
    return [...innerOperations, ...commonItem]
  }, [isEditKeys])

  const operationClick = useCallback((record, target, event) => {
    // console.log('record, target, event', record, target, event)
    console.log('record====', record)
    const { key } = target;
    const currentKey = record.key;
    if (key === 'save' || key === 'edit') {
      ref.current.editRow({
        rowKey: currentKey,
        edit: key === 'edit',
        callback: ({ isEditKeys, data }) => {
          setIsEditKeys(isEditKeys)
          // debugger
        }
      })
    } else if (key === 'del') {
      ref.current?.deleteData({
        rowKey: currentKey,
        callback: () => {
          console.log(ref.current?.getDeleteRowKeys())
        }
      })
    } else if (key === 'cancel') {
      ref.current?.cancel({ rowKey: currentKey }) //  取消 saveRowData(record) 原始数据
    } else if (key === "child") {
      ref.current.addRowChild({
        posRowKey: currentKey,
        callback: ({ data, isEditKeys }) => {
          console.log('isEditKeys', expandedRowKeys, isEditKeys)
          setExpandedRowKeys([...expandedRowKeys, currentKey])
          setIsEditKeys(isEditKeys)
        }
      })
    } else if (key === "copyData") {
      ref.current.addRowAfter({
        posRowKey: currentKey,
        rowData: [
          {
            ...record,
            key: Math.random().toString(36).substr(2, 5)

          }
        ],
        callback: (data, isEditKeys) => {
          console.log('isEditKeys', isEditKeys)
          setIsEditKeys(isEditKeys)
        }
      })
    } else if (key === "before") {
      ref.current.addRowBefore({
        posRowKey: currentKey,
        callback: ({ data, isEditKeys }) => {
          console.log('isEditKeys', isEditKeys)
          setExpandedRowKeys([...expandedRowKeys, currentKey[0]])
          setIsEditKeys(isEditKeys)
        }
      })
    } else if (key === 'after') {
      ref.current.addRowAfter({
        posRowKey: currentKey,
        callback: ({ data, isEditKeys }) => {
          console.log('isEditKeys', isEditKeys)
          setExpandedRowKeys([...expandedRowKeys, currentKey[0]])
          setIsEditKeys(isEditKeys)
        }
      })
    } else if (key === 'up') {
      ref.current.rowMoveTo({
        rowKey: currentKey,
        pos: -1
      })
    } else if (key === "down") {
      ref.current.rowMoveTo({
        rowKey: currentKey,
        pos: 1
      })
    }
  }, [isEditKeys, expandedRowKeys])

  return (
    <div style={{ height: '100%' }}>
      
      {/* <YNFLoader */}
      {/* <Modal visible={true} size={"lg"} className="editTableModal" > */}
        <div style={{ width: "100%", display: "flex", justifyContent: "flex-end", marginBottom: 16 }}>
        <Space>

          <Button onClick={addDataFirst} >首行添加</Button>
          <Button onClick={addDataLast} >尾行添加</Button>
          <Button onClick={copyRowDataBatch} >批量复制</Button>
          <Button onClick={delRowDataBatch}>批量删除</Button>
        </Space>

      </div>
<ConfigProvider>
        <EditTable
          fillSpace
          className={'edit-demo'}
          columns={columns}
          type={"inline"}
          data={data}
          expandable={
            {
              expandedRowKeys,
              onExpand: (expanded, record) => {
                if (expanded) {
                  setExpandedRowKeys([...expandedRowKeys, record.key])
                } else {
                  setExpandedRowKeys(expandedRowKeys.filter(item => item !== record.key))
                }
              }
            }
          }

          //  autoEditedByClickRows={false}
          ref={ref}
          autoCheckedByClickRows={false}

          // contextMenuVisible
          onPopMenuClick={onPopMenuClick}
          rowSelection={rowSelection}
          operationItems={operationItems}
          operationClick={operationClick}
          autoEditedByClickRows={false}
          // autoEditedByClickRows={"hover"}
          // autoSavedOnRowHoverOut={true}


          // rowActiveKey
          // rowDraggAble={true}
          isSum={false}
          rowKey={'key'}
        />
      </ConfigProvider>
      {/* </Modal> */}
         
      
      

    </div>

  );
}

export default EditTableDemo;
```
