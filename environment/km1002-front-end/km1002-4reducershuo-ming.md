# Reducer说明：

目前的Reducer主要分为两部分，全局的：

```
src/shared/reducers.js
```

局部的Reducer，局部的Reducer一般通过Epic和Types来实现，实现过程中一般位于三个核心组件目录中，文件名固定：

* `Act.Types.js`
* `Act.Epic.js`

这两个文件名会被工具扫描到，然后打包到连接文件`src/shared/datum.js`中，这个文件会被`src/entry/datum.js`连接

## 初始化状态

初始化状态的文件只有一个`src/shared/state.js`：

```js
import { DataLabor} from "../model"
export default {
    items: DataLabor.getObject({}),
    selected: DataLabor.getArray([]),
    filters: DataLabor.getObject(),
    detail: DataLabor.getObject(),
    documents: DataLabor.getArray([]),
    app:{
        buyers: DataLabor.getArray(),
        departments: DataLabor.getArray()
    }
}
```

上边文件定义了完整的状态信息，数据节点中的数据结构可参考TypeScript中的Model用法

## 状态节点含义

状态说明如下：

| 节点 | 含义 |
| :--- | :--- |
| app | 当前App应用配置数据节点，来自SYS\_APP表 |
| nav | 顶部导航栏数据 |
| menu | 左侧主菜单数据 |
| aside | 左侧【个人中心】主菜单数据 |
| page | 菜单效果专用数据，对应关系如下 |
| page -&gt; active | 当前主菜单选中id |
| page -&gt; aside | 当前最终子菜单选中的id |
| page -&gt; openKeys | 目前已经打开的父菜单id集合 |
| content -&gt; form | 表单专用状态节点 |
| env -&gt; hotel | 系统信息专用数据节点 |

## 状态树说明

![](/assets/KM1002/002.png)

状态树主要包含四个主要节点：

```javascript
export default combineReducers({
    routing: routerReducer,
    form: formReducer,
    "do": createEpics(),
    // Web Flow专用函数
    out
});
```

* routing：React-Router专用的状态树
* form：Redux-Form专用的状态树
* do：Epic专用状态树
* out：Vie-Ui专用状态树



