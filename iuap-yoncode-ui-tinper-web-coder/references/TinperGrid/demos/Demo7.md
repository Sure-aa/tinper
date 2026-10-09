---
tags:
  - TinperNextPro
  - TinperGrid组件
---
# TinperGrid 表格

## 基础编辑
双击单元格启动编辑，支持文本、数字、下拉选择等编辑器，编辑记录批量提交

```jsx
import React, { useState, useRef } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { EditModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/edit';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([EditModule, RowNumbersModule]);

export default function() {
  const gridRef = useRef(null);
  const [data, setData] = useState([
    { id: 1, name: '张三', age: 25, role: 'admin', email: 'zhangsan@example.com' },
    { id: 2, name: '李四', age: 30, role: 'user', email: 'lisi@example.com' },
    { id: 3, name: '王五', age: 28, role: 'user', email: 'wangwu@example.com' },
    { id: 4, name: '赵六', age: 35, role: 'admin', email: 'zhaoliu@example.com' },
    { id: 5, name: '孙七', age: 22, role: 'user', email: 'sunqi@example.com' },
  ]);

  const handleEditCommit = async (edits) => {
    console.log('[Demo] Batch commit:', edits);
    return true;
  };

  const columnDefs = [
    {
      field: 'name', headerName: '姓名', width: 150,
      editable: true, editor: 'text',
      editorParams: { placeholder: '请输入姓名', maxLength: 20 },
    },
    {
      field: 'age', headerName: '年龄', width: 120,
      editable: true, editor: 'number',
      editorParams: { min: 0, max: 150, placeholder: '请输入年龄' },
    },
    {
      field: 'role', headerName: '角色', width: 120,
      editable: true, editor: 'select',
      editorParams: {
        options: [
          { label: '管理员', value: 'admin' },
          { label: '普通用户', value: 'user' },
        ],
      },
    },
    {
      field: 'email', headerName: '邮箱', width: 220,
      editable: true, editor: 'text', singleClickEdit: true,
      editorParams: { placeholder: '请输入邮箱' },
    },
  ];

  const handleCommitAll = async () => {
    const api = gridRef.current?.api;
    if (!api) return;
    const pendingEdits = api.getPendingEdits();
    if (pendingEdits.length === 0) { alert('没有待提交的编辑'); return; }
    const success = await api.commitAllEdits();
    alert(success ? `成功提交 ${pendingEdits.length} 个编辑` : '提交失败');
  };

  const handleCancelAll = () => {
    const api = gridRef.current?.api;
    if (!api) return;
    const pendingEdits = api.getPendingEdits();
    if (pendingEdits.length === 0) { alert('没有待取消的编辑'); return; }
    api.cancelAllEdit();
    alert(`已取消 ${pendingEdits.length} 个编辑`);
  };

  return (
    <div>
      <h2>基础编辑</h2>
      <p style={{ color: '#666', marginBottom: 10 }}>
        双击单元格启动编辑，修改后按 Enter 或失焦关闭编辑器。邮箱列单击即可编辑。
      </p>
      <div style={{ marginBottom: 16 }}>
        <button onClick={() => { const api = gridRef.current?.api; if (api) alert(`共有 ${api.getPendingEdits().length} 个待提交的编辑`); }} style={{ marginRight: 8 }}>查看待提交编辑</button>
        <button onClick={handleCommitAll} style={{ marginRight: 8, backgroundColor: '#1890ff', color: 'white', border: 'none', padding: '6px 12px', borderRadius: 4, cursor: 'pointer' }}>提交所有编辑</button>
        <button onClick={handleCancelAll} style={{ backgroundColor: '#ff4d4f', color: 'white', border: 'none', padding: '6px 12px', borderRadius: 4, cursor: 'pointer' }}>取消所有编辑</button>
      </div>
      <Grid
        ref={gridRef}
        data={data}
        columnDefs={columnDefs}
        width={800}
        height={400}
        rowHeight={40}
        onEditCommit={handleEditCommit}
        showRowNum={true}
      />
    </div>
  );
}
```

## 编辑验证
支持同步验证和异步验证，验证失败时显示错误提示并阻止提交

```jsx
import React, { useState, useRef } from 'react';
import { Grid, ModuleRegistry } from 'tne-tinpernextpro-fe/TinperGrid';
import { EditModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/edit';
import { RowNumbersModule } from 'tne-tinpernextpro-fe/TinperGrid/modules/rownumbers';

ModuleRegistry.registerModules([EditModule, RowNumbersModule]);

export default function() {
  const gridRef = useRef(null);
  const [data] = useState([
    { id: 1, name: '张三', age: 25, email: 'zhangsan@example.com', phone: '13800138000' },
    { id: 2, name: '李四', age: 30, email: 'lisi@example.com', phone: '13900139000' },
    { id: 3, name: '王五', age: 28, email: 'wangwu@example.com', phone: '13700137000' },
  ]);

  const checkEmailExists = async (email) => {
    await new Promise((resolve) => setTimeout(resolve, 500));
    return ['test@example.com', 'admin@example.com'].includes(email);
  };

  const columnDefs = [
    {
      field: 'name', headerName: '姓名', width: 150, editable: true, editor: 'text',
      validator: ({ value }) => {
        if (!value || value.trim() === '') return { valid: false, message: '姓名不能为空' };
        if (value.length < 2) return { valid: false, message: '姓名至少2个字符' };
        return { valid: true };
      },
    },
    {
      field: 'age', headerName: '年龄', width: 120, editable: true, editor: 'number',
      editorParams: { min: 0, max: 150 },
      validator: ({ value }) => {
        const age = Number(value);
        if (isNaN(age)) return { valid: false, message: '请输入有效的数字' };
        if (age < 18) return { valid: false, message: '年龄不能小于18岁' };
        if (age > 65) return { valid: false, message: '年龄不能大于65岁' };
        return { valid: true };
      },
    },
    {
      field: 'email', headerName: '邮箱', width: 220, editable: true, editor: 'text',
      validator: async ({ value }) => {
        if (!value || value.trim() === '') return { valid: false, message: '邮箱不能为空' };
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)) return { valid: false, message: '邮箱格式不正确' };
        const exists = await checkEmailExists(value);
        if (exists) return { valid: false, message: '该邮箱已被使用' };
        return { valid: true };
      },
    },
    {
      field: 'phone', headerName: '手机号', width: 150, editable: true, editor: 'text',
      validator: ({ value }) => {
        if (!value || value.trim() === '') return { valid: false, message: '手机号不能为空' };
        if (!/^1[3-9]\d{9}$/.test(value)) return { valid: false, message: '请输入正确的手机号' };
        return { valid: true };
      },
    },
  ];

  return (
    <div>
      <h2>编辑验证</h2>
      <p style={{ color: '#666', marginBottom: 10 }}>
        姓名：必填至少2字符；年龄：18-65岁；邮箱：格式+异步唯一性（test@example.com 已存在）；手机号：1开头11位
      </p>
      <div style={{ marginBottom: 16 }}>
        <button onClick={async () => {
          const api = gridRef.current?.api;
          if (!api) return;
          const success = await api.commitAllEdits();
          alert(success ? '提交成功 ✅' : '提交失败 ❌，请检查验证错误');
        }}>提交所有编辑</button>
      </div>
      <Grid ref={gridRef} data={data} columnDefs={columnDefs} width={800} height={300} rowHeight={40} showRowNum={true} />
    </div>
  );
}
```
