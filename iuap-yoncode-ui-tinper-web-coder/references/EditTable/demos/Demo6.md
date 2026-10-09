---
tags:
  - TinperNextPro
  - EditTable组件
---
# EditTable 编辑表格

## 列数据联动效果
继承于TinperNext-EditTable组件。

```jsx
import { useRef, useState, useEffect, useMemo, useCallback } from "react";
import { EditTable } from "tne-tinpernextpro-fe";

import { data } from "./mock";

const { Button, Space } = window.TinperNext;

const DefineTreeEditTabele = (props) => {
  const ref = useRef();

  const [isEditKeys, setIsEditKeys] = useState([]);
  const [expandedRowKeys, setExpandedRowKeys] = useState([]);
  const [dataSource, setDataSource] = useState(data);

  const [extendColumns, setExtendColumns] = useState([
    {
      title: "2024年1月",
      dataIndex: "2024-01",
      key: "2024-01",
      width: 100,
      editType: "number",
      sumCol: true
    },
    {
      title: "2024年2月",
      dataIndex: "2024-02",
      key: "2024-02",
      width: 100,
      editType: "number",
      sumCol: true
    },
    {
      title: "2024年3月",
      dataIndex: "2024-03",
      key: "2024-03",
      width: 100,
      editType: "number",
      sumCol: true
    },
    {
      title: "2024年4月",
      dataIndex: "2024-04",
      key: "2024-04",
      width: 100,
      editType: "number",
      sumCol: true
    },
    {
      title: "2024年5月",
      dataIndex: "2024-05",
      key: "2024-05",
      width: 100,
      editType: "number",
      sumCol: true
    }
  ]);

  useEffect(() => {
    setExpandedRowKeys(data.map((e) => e.id));
  }, []);

  const rowSum = (record, column, value) => {
    const { parent, id } = record;
    const row = ref.current?.getRowDataByKey({ key: parent })?.[0];
    if (row.bl_sum === "0") return;
    const sum = row?.children?.reduce((pre, cur) => {
      return cur?.dr + pre;
    }, 0);
    ref.current?.saveMultiCellData({
      rowData: { ...row, dr: Math.floor(Math.random() * 10) },
      callback: (newData) => {
        setDataSource(newData)
      }
    });
  };

  const columns = useMemo(() => {
    return [
      {
        title: "序号",
        dataIndex: "orderno",
        key: "orderno",
        width: 140,
        editAbled: false
      },
      {
        title: "内容",
        dataIndex: "name",
        key: "name",
        width: 260,
        editType: "input"
      },
      {
        title: "预算金额(元)",
        dataIndex: "dr",
        key: "dr",
        width: 150,
        editType: "number",
        editAbled: ({ bl_sum }) => {
          return bl_sum === "0";
        },
        render (text) {
          return text
        },
        onCellChange: (record, column, value) => {
          rowSum(record, column, value);
        },
        sumCol: true
      },
      {
        key: "zhanwei",
        editAbled: false
      }
      // ...extendColumns,
    ];
  }, [isEditKeys, extendColumns]);

  const operationItems = useCallback(
    (record, index, isEdit, innerOperations) => {
      const commonItem = [
        {
          key: "del",
          text: "删除"
        },
        {
          key: "child",
          text: "插入子级"
        },
        {
          key: "copyData",
          text: "复制行"
        }
      ];
      return [];
    },
    [isEditKeys]
  );

  const operationClick = useCallback(
    (record, target, event) => {
      // console.log('record, target, event', record, target, event)
      console.log("record====", record);
      const { key } = target;
      const currentKey = record.id;
      if (key === "del") {
        ref.current?.deleteData({
          rowKey: currentKey,
          callback: () => {
            console.log(ref.current?.getDeleteRowKeys());
          }
        });
      } else if (key === "child") {
        ref.current.addRowChild({
          posRowKey: currentKey,
          callback: ({ data, isEditKeys }) => {
            console.log("isEditKeys", expandedRowKeys, isEditKeys);
            setExpandedRowKeys([...expandedRowKeys, currentKey]);
            setIsEditKeys(isEditKeys);
          }
        });
      } else if (key === "copyData") {
        ref.current.addRowAfter({
          posRowKey: currentKey,
          rowData: [
            {
              ...record,
              id: Math.random().toString(36).substr(2, 5)
            }
          ],
          callback: (data, isEditKeys) => {
            console.log("isEditKeys", isEditKeys);
            setIsEditKeys(isEditKeys);
          }
        });
      }
    },
    [isEditKeys, expandedRowKeys]
  );
  function getData () {
    console.log(ref.current.getAllData(), "全部数据");
  }

  function setColumnData () {
    ref.current.saveColumnData({
      dataIndex: "dr",
      cellValue: 0
    })
  }

  return (
    <div style={{ height: "50vh" }}>
      <div style={{ width: "100%", display: "flex", justifyContent: "flex-end", marginBottom: 16 }}>
        <Space>
          <Button onClick={getData}>获取全部数据</Button>
          <Button onClick={setColumnData}>设置列值</Button>
        </Space>
      </div>
      <EditTable
        openSelectCells
        columns={columns}
        type={"inline"}
        data={dataSource}
        expandable={{
          expandedRowKeys,
          onExpand: (expanded, record) => {
            if (expanded) {
              setExpandedRowKeys([...expandedRowKeys, record.id]);
            } else {
              setExpandedRowKeys(expandedRowKeys.filter((item) => item !== record.id));
            }
          }
        }}
        ref={ref}
        autoCheckedByClickRows={false}
        operationItems={operationItems}
        operationClick={operationClick}
        autoEditedByClickRows="hover"
        isSum={false}
        showSum={["total"]}
        rowKey={"id"}

      />
    </div>
  );
};

export default DefineTreeEditTabele;
```
