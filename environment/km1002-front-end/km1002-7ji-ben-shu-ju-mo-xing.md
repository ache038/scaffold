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



