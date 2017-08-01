# 状态读

```
StateOut，一般该对象仅在Act.Orbit.js文件中的StateToProp中使用
```

状态读取是整个框架中最复杂的一部分，主要是考虑到不同情况下的状态解析问题，并通过路径统一实现状态的多种不同方式的读取，先看看下边脚本：

```javascript
const indexS2P = (state) => {
    const response = DataLabor.createOut(state);
    const data = response.revamp(['app']).rework({
        'datum': ['hotel']
    }).to();
    // render的专用计算，用于检查哪些节点是需要计算成render值的
    // *：这些节点都是自定义结构，所以需要保证每个节点都有is方法
    const $ready = response.ready(
        {
            'app':true,
            'datum':['hotel'],
            'layout':['nav','menu','aside']
        });
    return {
        ...data,
        $ready
    }
};
```

## 1.构造

```javascript
const response = DataLabor.createOut(state);
```

## 2.读取

状态读取主要有两个方法：`revamp, rework`

### 一级节点读取revamp

如果直接读取一级多个状态树的根节点信息，则可直接使用revamp方法，如下边代码：

```javascript
const data = response.revamp(['app','user']).to();
```

上边代码将会从状态树上读取节点：`out.app`和`out.user`生成的data数据结构如：

```json
{
    $app:"DataObject/DataArray",
    $user:"DataObject/DataArray"
}
```

数据结构类型只可能是DataContainer，具体数据模型参考：[KM1002 - 7.基本数据模型](/environment/km1002-front-end/km1002-7ji-ben-shu-ju-mo-xing.md)

### 多级节点读取rework

如果需要从多级状态树中读取，则可使用rework方法，参考下边代码：

```js
const data = response.revamp(['app']).rework({
    'datum': ['hotel'],
    'layout': ['nav','menu','aside']
}).to();
```

上边的代码会读取下边节点的信息：

* `out.datum.hotel`
* `out.layout.nav`
* `out.layout.menu`
* `out.layout.aside`

然后生成的data的数据结构如：

```json
{
    $hotel:"DataObject/DataArray",
    $nav:"DataObject/DataArray",
    $menu:"DataObject/DataArray",
    $aside:"DataObject/DataArray"
}
```

### 判断是否加载完成方法：ready

ready方法会判断对应节点的数据结构中ready是否为true（即是否最新），参数同rework，这里不重复介绍。

