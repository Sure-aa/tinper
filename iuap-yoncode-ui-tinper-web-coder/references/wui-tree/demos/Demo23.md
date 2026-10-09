---
tags:
  - TinperNext
  - tree组件
---
# 树形控件 Tree

## Shift 连选示例

展示勾选状态在 Shift 连选下的表现，并支持切换父子是否关联、收起父级是否包含子级。

```tsx
import { Tree, TreeProps, Switch, Tag } from '@tinper/next-ui';
import React, { useCallback, useMemo, useState } from 'react';

const { TreeNode } = Tree;

const x = 6;
const y = 5;
const z = 2;

type GlobalDataType = {
    title: string;
    key: string;
    children?: GlobalDataType;
}[];

const gData: GlobalDataType = [];

const generateData = (_level: number, _preKey?: string, _tns?: GlobalDataType) => {
    const preKey = _preKey || '0';
    const tns = _tns || gData;

    const children: string[] = [];
    for (let i = 0; i < x; i++) {
        const key = `${preKey}-${i}`;
        tns.push({ title: key, key });
        if (i < y) {
            children.push(key);
        }
    }
    if (_level < 0) {
        return tns;
    }
    const level = _level - 1;
    children.forEach((key, index) => {
        tns[index].children = [];
        return generateData(level, key, tns[index].children);
    });
};
generateData(z);

const Demo23 = () => {
    const [expandedKeys, setExpandedKeys] = useState<string[]>(['0-0', '0-0-0']);
    const [autoExpandParent, setAutoExpandParent] = useState<boolean>(true);
    const [checkedKeys, setCheckedKeys] = useState<string[]>([]);
    const [checkStrictly, setCheckStrictly] = useState<boolean>(false);
    const [strictRangeHasFolded, setStrictRangeHasFolded] = useState<boolean>(false);

    const handleExpand: TreeProps['onExpand'] = useCallback((keys) => {
        setExpandedKeys(keys);
        setAutoExpandParent(false);
    }, []);

    const handleCheck: TreeProps['onCheck'] = useCallback((keys) => {
        setCheckedKeys(keys as string[]);
    }, []);

    const handleStrictToggle = useCallback((value: boolean) => {
        setCheckStrictly(value);
        if (!value) {
            setStrictRangeHasFolded(false);
        }
    }, []);

    const renderNodes = useMemo(() => {
        const loop = (data: GlobalDataType): React.ReactNode =>
            data.map((item) => {
                if (item.children) {
                    return (
                        <TreeNode key={item.key} title={item.key}>
                            {loop(item.children)}
                        </TreeNode>
                    );
                }
                return <TreeNode key={item.key} title={item.key} isLeaf />;
            });
        return loop(gData);
    }, []);

    return (
        <div>
            <div style={{ marginBottom: 12, lineHeight: '24px' }}>
                <Tag style={{ marginRight: 12 }}>
                    Shift + 点击复选框
                </Tag>
                支持区间勾选，受 `checkStrictly` 和 `strictRangeHasFolded` 控制。
            </div>
            <div style={{ marginBottom: 8 }}>
                <span style={{ marginRight: 8 }}>父子不关联（checkStrictly）：</span>
                <Switch checked={checkStrictly} onChange={handleStrictToggle} />
            </div>
            <div style={{ marginBottom: 16 }}>
                <span style={{ marginRight: 8 }}>收起父级仍包含子级（strictRangeHasFolded）：</span>
                <Switch
                    disabled={!checkStrictly}
                    checked={strictRangeHasFolded}
                    onChange={(value: boolean) => setStrictRangeHasFolded(value)}
                />
            </div>

            <Tree
                checkable
                showLine
                checkStrictly={checkStrictly}
                strictRangeHasFolded={strictRangeHasFolded}
                expandedKeys={expandedKeys}
                autoExpandParent={autoExpandParent}
                onExpand={handleExpand}
                onCheck={handleCheck}
                checkedKeys={checkedKeys}
            >
                {renderNodes}
            </Tree>
        </div>
    );
};

export default Demo23;
```
