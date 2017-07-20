# Reducer说明

所有Reducer文件位于下边目录：

```
src/redux/reducers/
```

## 初始化状态

初始化状态的两个文件路径如下：

```
OOB状态文件：src/redux/reducers/Out.json
Ext应用状态文件：src/shared/state.json
```

vie-ui的状态文件包含两部分，OOB和Ext分别对应标准vie-ui的状态以及扩展状态，标准状态针对所有的应用结构都是一致的，而Ext部分则是根据不同的应用用来存储不同的基础数据，如下边代码段中的hotel节点，只有在当前酒店管理系统中使用到。

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

