---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础展开行
通过 expandedRowRender 自定义展开行内容，支持受控模式管理展开状态

```jsx
import React, { useState } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { ExpandModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/expand';

ModuleRegistry.registerModules([ExpandModule]);

export default function BasicExpandRowDemo() {
  const [expandedKeys, setExpandedKeys] = useState(['1', '3']);

  const data = [
    { id: '1', name: '张三', age: 28, department: '技术部', email: 'zhangsan@example.com', phone: '13800138001', address: '北京市朝阳区xxx路', joinDate: '2020-03-15', skills: ['React', 'TypeScript', 'Node.js'] },
    { id: '2', name: '李四', age: 32, department: '产品部', email: 'lisi@example.com', phone: '13800138002', address: '上海市浦东新区xxx路', joinDate: '2019-06-20', skills: ['产品设计', '用户研究', '数据分析'] },
    { id: '3', name: '王五', age: 25, department: '设计部', email: 'wangwu@example.com', phone: '13800138003', address: '广州市天河区xxx路', joinDate: '2021-01-10', skills: ['UI设计', 'Figma', 'Sketch'] },
    { id: '4', name: '赵六', age: 30, department: '技术部', email: 'zhaoliu@example.com', phone: '13800138004', address: '深圳市南山区xxx路', joinDate: '2018-09-01', skills: ['Java', 'Spring', 'MySQL'] },
  ];

  const columnDefs = [
    { field: 'name', headerName: '姓名', width: 120 },
    { field: 'age', headerName: '年龄', width: 80, align: 'center' },
    { field: 'department', headerName: '部门', width: 120 },
    { field: 'email', headerName: '邮箱', width: 200 },
  ];

  const expandedRowRender = (record) => (
    <div style={{ padding: '16px 24px', background: '#fafafa', height: 200 }}>
      <h4 style={{ margin: '0 0 12px 0' }}>详细信息</h4>
      <div style={{ display: 'grid', gridTemplateColumns: '1fr 1fr', gap: '8px' }}>
        <div><strong>电话：</strong>{record.phone}</div>
        <div><strong>入职日期：</strong>{record.joinDate}</div>
        <div><strong>地址：</strong>{record.address}</div>
        <div>
          <strong>技能：</strong>
          {record.skills?.map((skill, i) => (
            <span key={i} style={{ display: 'inline-block', padding: '2px 8px', margin: '2px 4px 2px 0', background: '#e6f7ff', borderRadius: 4, fontSize: 12 }}>{skill}</span>
          ))}
        </div>
      </div>
    </div>
  );

  return (
    <div>
      <h3>基础展开行</h3>
      <div style={{ marginBottom: 16 }}>当前展开的行：<code>{JSON.stringify(expandedKeys)}</code></div>
      <Grid
        data={data}
        columnDefs={columnDefs}
        rowKey="id"
        width={700}
        height={400}
        expandedRowRender={expandedRowRender}
        expandedRowKeys={expandedKeys}
        showExpandColumn={true}
        onExpandedRowsChange={(keys) => setExpandedKeys(keys.map(String))}
      />
    </div>
  );
}
```
