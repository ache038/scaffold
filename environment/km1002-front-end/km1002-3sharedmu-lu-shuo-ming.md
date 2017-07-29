# Shared目录说明

```
src/shared
```

Shared目录主要包含以下几大类信息

* `lg.js`：中文语言包，该语言包和HOC组件I18nComponent绑定，当一个组件需要支持多语言环境时则直接从lg.js中读取语言加载函数（该函数目前只会被I18nComponent使用）；
* `global.less/sco.less`：CSS全局配置，之中包含了颜色定义、字体定义、可共享的全局CSS定义等【特别是颜色信息，所有的颜色信息都保存在global.less中，最后的应用呈现的“风格”依赖于该文件中定义的全局色彩、字体等】
* `actions.js`：全局使用的Action Types定义——需要使用全局Action时改动，配合reducers.js文件；
* `reducers.js`：全局使用的Reducer文件——该文件会默认被导入，定义了actions中的实现；
* `routes.js`：Redux-Router使用的入口路由文件；
* `state.js`：初始化状态文件；
* `datum.js`：【系统生成】生成的连接文件，该文件不在git托管中，不同开发人员生成内容不同，目前该文件已经在启动脚本中生成了，所以不需要手工执行工具脚本来生成。

## Shared连接入口

```
src/lib/index.js
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
    // 共享资源文件
    Lg,             // 资源文件语言包，引入I18nComponent过后可直接取消该资源文件的引用
    UI,             // 可重用组件库
    Types,          // 全局Redux Type
    Config,         // 全局配置Json数据文件
}
```

Less文件的导入一般在内部的`.less`文件中使用头部导入

```less
@import '../../shared/global';
```

* 资源文件分为两部分：Lg为语言包，该语言包和全局配置中的配置项lang对应，Icon为图标包，语言包会根据全局配置中的语言读取对应目录中的资源文件，文件名和组件名保持一致；
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



