# environment目录说明

```
src/environment
```

environment目录主要包含以下几大类信息

* `index.js`：环境入口文件，该文件用于连接所有应用需要使用的资源文件，Model除外
* `actions.js`：全局使用的Action Types定义——需要使用全局Action时改动，配合reducers.js文件；
* `reducers.js`：全局使用的Reducer文件——该文件会默认被导入，定义了actions中的实现；
* `routes.js`：Redux-Router使用的入口路由文件；
* `state.js`：初始化状态文件；
* `datum.js`：【系统生成】生成的连接文件，该文件不在git托管中，不同开发人员生成内容不同，目前该文件已经在启动脚本中生成了，所以不需要手工执行工具脚本来生成。

## index.js连接点

![](/assets/KM1002/002.png)

| 连接点简介 | 备注 |
| :--- | :--- |
| vie-joy | 用于连接vie-joy的工具库，但工具库本身不从index.js导出，vie-joy工具库的连接目的只是为了初始化$app, $public, $secure, $oauth四个核心全局变量 |
| src/environment/actions.js | 当前应用需要使用的Redux全局Actions |
| src/config.json -&gt; $config | 全局配置文件，转移到变量$config，调用方法和$app这一类方法一致 |
| src/combination/index.js | Hoc组件的入口文件 |
| src/control/index.js | 可重用的Web组件的入口文件 |
| src/lang/index.js | 当前应用使用的语言包资源文件 |
| src/environment/icon/index.js | 当前应用使用的Icon图标包资源文件 |
| $app | Application全局配置类 |
| $public | 非安全模式的Promise生成类 |
| $secure | 安全模式的Promise生成类（带Token的请求） |
| $oauth | 系统专用OAuth类，用于登陆、注销、控制、签名等 |

## index.js文件解析

```
src/environment/index.js
```

该文件为统一工具目录，之中包含的资源文件如下：

```javascript
import Types from '../shared/actions'
import Config from '../config.json'
import UI from '../control'
import Log from './log'
import Lg from '../shared/lg'
...
export default {
    ...
    // 资源文件
    Lg,             // 资源文件语言包，引入I18nComponent过后可直接取消该资源文件的引用
    UI,             // 可重用组件库
    Types,          // 全局Redux Type
    Config,         // 全局配置Json数据文件
    Log,            // 调试专用日志处理器
}
```

Less文件的导入一般在内部的`.less`文件中使用头部导入语法

```less
@import '../../shared/global';
```

* 资源文件Lg不会被开发代码直接引用，引入了`I18nComponent`的Hoc组件过后，该资源文件会被它默认读取并和对应的组件实现绑定；
* 全局使用的Reducer/Action主要包含在：`actions.js`和`reducers.js`中，一般不带任何业务意义，目前为回写状态树共享；
* `routes.js`是react-router中需要使用的路由包，添加新的路由页面时候才会需要修改该文件；
* `state.js`为初始化全局状态文件，初始化Redux状态树专用

## datum.js生成文件

`datum.js`文件是依靠nodejs的工具生成的，该生成文件充当了连接器的作用，用于连接每一个组件中的两个特殊文件：`Act.Types.js`和`Act.Epic.js`，让所有的组件在使用Reducer的过程中在内部实现一个闭环。

```javascript
import _yOBE69tW5b0uEpic from '../container/login/Act.Epic.js';
import _ngqHvxQFa4LxEpic from '../container/main/Act.Epic.js';
import _GQw76Mb2V3xnTypes from '../container/login/Act.Types.js';
import __STwG_VBZwaUTypes from '../container/main/Act.Types.js';

import types from './actions';
export default {
    handlers:{
        ..._GQw76Mb2V3xnTypes,
        ...__STwG_VBZwaUTypes,
        ...types
    },
    epics:{
        ..._yOBE69tW5b0uEpic,
        ..._ngqHvxQFa4LxEpic,
    }
}
```

这个文件会连接container，components目录下的所有Epic和Reducer组件，并export给entry/datum.js中的文件进行连接，那么最大的好处是：开发人员可以只集中在组件目录下开发下列四种组件：

* container：容器组件
* control：可共享组件（一般不带状态）
* components：页面组件
* combination：Hoc组件



