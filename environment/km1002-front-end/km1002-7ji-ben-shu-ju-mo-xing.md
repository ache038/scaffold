# 基本数据模型

```
src/entity/data/**.ts
```

目前设计的前端基本数据模型主要包含三种：

* DataObject
* DataArray
* DataTree

这些数据模型都实现了DataContainer接口：

```typescript
/**
 * 接口基础类型
 */
interface DataContainer{

    ready: boolean;

    _(key: any): any;

    is(): boolean;

    raw(): Object;

    get(): any;
}

export default DataContainer
```

Object

```json
{
    ready:"Boolean值，用于标识当前DataObject是否最新数据，false则可能触发重新加载",
    data:{}
}
```

Array

```json
{
    ready:"Boolean值，用于标识当前DataArray是否最新数据，false则可能触发重新加载",
    data:"JSON.stringify序列化后的原始字符串，主要目的是在状态树上不展开，用单节点呈现",
    length: "Number值，当前Array的长度"
}
```

Tree

```json
{
    ready:"Boolean值，用于标识当前DataTree是否最新数据",
    data:"原始数组JSON.stringify序列化后的字符串",
    tree:"当前Tree的模型，为一个数组"
}
```

TreeNode：该结构位于Tree内部

```json
{
    key:"当前TreeNode的标识",
    parent:"当前TreeNode的父节点id",
    children:"当前TreeNode的子节点列表，一个Array的结构"
}
```



