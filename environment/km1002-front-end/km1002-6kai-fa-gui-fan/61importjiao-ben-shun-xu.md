# Import顺序

对于每一个开发的组件而言，import的顺序整体统一，一般按照下边格式：

```javascript
// React主要库文件
import React from "react";

// 第三方库文件如：moment, random-js, immutable

// 内置less文件导入（风格），风格文件第一个都是UI.less，其他次之
import "./UI.less";
import "./UI.Auto.less";

// 工具包入口导入
import Fn from "../../lib";

// 当前组件内的Act文件导入
import event from "./Act.Event";
import redux from "./Act.Orbit";
import ui from './Act.UI'

// 子组件导入
import Nav from "./UI.Header";
import Bottom from "./UI.Footer";
import User from "./UI.User";
import Menu from "./UI.Menu";

// Ant Design核心组件导入
import {
    Layout
} from "antd";

// Ant Design二级组件导入
const {
    Header,
    Footer,
    Sider,
    Content
} = Layout;
```



