# Import顺序

对于每一个开发的组件而言，import的顺序整体统一，一般按照下边格式：

```javascript
// 第三方组件库
import React from "react";

// 导入自己开发的vie-joy工具包
import {Loch, Une} from "vie-joy";

// 导入当前组件需要使用的Less风格文件
import "./UI.less";
import "./UI.Auto.less";

// 导入combination/control两种特殊组件
import {LoadingLayout,LogComponent} from '../../environment'

// 导入其他environment环境文件
import {$app} from '../../environment'

// 导入TypeScript中的数据模型
import {DataLabor} from '../../entity'

// 导入redux和Event，变量名固定
import Event from "./Act.Event";
import redux from "./Act.Orbit";

// 导入子组件
import Nav from "./UI.Header";
import Bottom from './UI.Footer';
import User from './UI.User'
import Menu from './UI.Menu'

// 导入Ant Design组件
import {Layout} from "antd";

// 从Ant Design中抽取子组件
const {
    Header,
    Footer,
    Sider,
    Content
} = Layout;
// 为当前组件命名——注：该名称将会在I18nComponent高阶组件中影响读取资源文件路径，尽可能统一
const Name = 'container.Main';
```

* Ant Design组件不放在同一行，形成每一行一个组件或多个组件的导入模式；
* 顺序严格按照上边的定义进行
* 固定的变量名遵循组件内的变量规范：[6.3.固定变量名](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/63gu-ding-bian-liang-ming.md)



