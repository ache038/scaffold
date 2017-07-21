# Shared目录说明

```
src/shared
```

Shared目录主要包含以下几大类信息

* `res.js`：中文语言包，图标包，全局使用的资源文件信息；
* `global.less`：CSS全局配置，之中包含了颜色定义、字体定义、可共享的全局CSS定义等【特别是颜色信息，所有的颜色信息都保存在global.less中，最后的应用呈现的“风格”依赖于该文件中定义的全局色彩、字体等】
* `actions.js`：全局使用的Action Types定义——需要使用全局Action时改动，配合reducers.js文件；
* `reducers.js`：全局使用的Reducer文件——该文件会默认被导入，定义了actions中的实现；
* `routes.js`：Redux-Router使用的入口路由文件；
* `state.js`：初始化状态文件；
* `datum.js`：【系统生成】生成的连接文件，该文件不在git托管中，不同开发人员生成内容不同；

## Shared连接入口

```
src/lib/index.js
```

该文件为统一工具目录，之中包含的资源文件如下：

```javascript
import Res from '../shared/res.js'
import Types from '../shared/actions'
import UI from '../control'
import Log from './log'
import Config from '../config.json'

...
export default {
    ...
    // 共享资源文件
    Lg: Res.Lg,         // 资源文件语言包
    UI,                 // 组件库
    Icon: Res.Icon,     // 全局图标文件
    Types,
    Config,
}
```

Less文件的导入一般在内部的`.less`文件中使用头部导入

```less
@import '../../shared/global';
```

* 资源文件分为两部分：Lg为语言包，该语言包和全局配置中的配置项lang对应，Icon为图标包；
* 全局使用的Reducer/Action主要包含在：`actions.js`和`reducers.js`中，一般不带任何业务意义，目前为回写状态树共享；
* `routes.js`是react-router中需要使用的路由包，添加新的路由页面时候才会需要修改该文件；
* state.js为



