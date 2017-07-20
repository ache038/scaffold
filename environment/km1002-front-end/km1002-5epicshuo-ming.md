# Epic说明

Epic负责所有的和后端交互的RxJs模块，其基础目录结构如下：

![](/assets/KM1002/003.png)

## 行为函数

epic目录中的文件为内部纯函数库，每个文件直接开放函数接口，并且不和任何Action相关；真正的Epic对应的Reducer组件在下边两个目录中：

* `ext`：扩展Epic，用于处理新应用的Reducer配置
* `oob`：标准库Epic，Engine专用多个应用可更像的Reducer配置

当前Epic的连接点在`index.js`文件中：

```javascript
import { combineEpics } from 'redux-observable'

// 全局
import App from './oob/Do.App'
// Ext
import Hotel from './ext/Do.Hotel'

export default {
    Epics:combineEpics(
        // 添加远程接口时必须方法
        App.fnApp,
        App.fnPreApp,
        // 酒店
        Hotel.fnHotel
    ),
    Handlers:{
        // 直接绑定远程接口的方法
        ...App,

        ...Hotel
    }
}
```

需要注意的是combinEpics在每次添加了Epic过后，需要将新函数添加到当前方法参数中。

