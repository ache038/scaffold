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

## index.js文件内容

```
src/environment/index.js
```

该文件为统一工具目录，之中包含的资源文件如下：

```javascript
import Config from '../config.json';
import {
    App,
    Promettre,
    OAuth
} from 'vie-joy';

export {default as Langue} from '../lang/index'             // Language语言包
export {default as Ikon} from './icon'                      // Ikon图标包信息
export {default as Taper} from './actions'                  // Types组件

// Hoc组件专用包
export {
    LogComponent,
    I18nComponent,
    FormComponent
} from '../combination'

// Web可重用组件包，包括Ant对话框
export {
    LoadingLayout,
    Dialog,
    Item
} from '../control'

// 专用连接，用于构造调试环境以及应用和Promise环境
export const $config = Config;
// 只在开发环境开启Promise的专用调试日志
const {endpoint, key} = Config;
export const isDebug = () => ('development' === process.env.NODE_ENV && $config.debug);
const debug = isDebug();
// 全局应用变量
export const $app = new App(Config['key'], Config['name']);
// 不带安全认证的Promise
export const $public = new Promettre({endpoint, key, debug}, false);
// 带安全认证的Promise
export const $secure = new Promettre({endpoint, key, debug});
// 用户认证专用接口连接
export const $oauth = new OAuth({endpoint, key, debug});
```

## datum.js生成文件

`datum.js`文件是依靠nodejs的工具生成的，该生成文件充当了连接器的作用，用于连接每一个组件中的两个特殊文件：`Act.Types.js`和`Act.Epic.js`，让所有的组件在使用Reducer的过程中在内部实现一个闭环。

```javascript
import _FZadJiIM__NZEpic from '../components/fore/Act.Epic.js';
import _R69W1KW09_bjEpic from '../container/login/Act.Epic.js';
import _IisOPUWe6aMkEpic from '../container/main/Act.Epic.js';
import _W1FtXkCivg9yTypes from '../components/fore/Act.Types.js';
import _okCiWc_z2FADTypes from '../container/login/Act.Types.js';
import _VKt02BTXfqgtTypes from '../container/main/Act.Types.js';

import types from './actions';
export default {
	handlers:{
		..._W1FtXkCivg9yTypes,
		..._okCiWc_z2FADTypes,
		..._VKt02BTXfqgtTypes,
		...types
	},
	epics:{
		..._FZadJiIM__NZEpic,
		..._R69W1KW09_bjEpic,
		..._IisOPUWe6aMkEpic,
	}
}
```

这个文件会连接container，components目录下的所有Epic和Reducer组件，并export给entry/datum.js中的文件进行连接，每次启动应用程序时候脚本会自动执行，如果有新的Types和Epic也会自动打包到当前文件中生成。



