# Reducer说明：

目前的Reducer主要分为两部分，全局的：

```
src/shared/reducers.js
```



## 初始化状态

初始化状态的两个文件路径如下：

```
OOB状态文件：src/redux/reducers/Out.json
Ext应用状态文件：src/shared/state.json
```

vie-ui的状态文件包含两部分，OOB和Ext分别对应标准vie-ui的状态以及扩展状态，标准状态针对所有的应用结构都是一致的，而Ext部分则是根据不同的应用用来存储不同的基础数据，如下边代码段中的hotel节点，只有在当前酒店管理系统中使用到。一般的数据节点都包含两部分，其数据格式基本如下：

```json
{
  "data":{},
  "inited":false
}
```

* data：数据内容节点，用于读取数据信息
* inited：数据加载节点，标识当前数据是否执行加载的专用标识
  * false：标识当前数据节点已经不是最新的，需要重新加载
  * true：当前数据节点已经是从远程读取的最新数据，不需要重新加载

### OOB

```json
{
  "app":{
    "data":{},
    "inited":false
  },
  "nav":{},
  "menu":{},
  "aside":{},
  "page":{
    "openKeys":[]
  },
  "content":{
    "form":{}
  }
}
```

### Ext

```json
{
  "env":{
    "hotel":{
      "inited":false,
      "data":{}
    }
  }
}
```

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
| env -&gt; hotel | 酒店管理系统酒店全局信息专用数据节点 |

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



