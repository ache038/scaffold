# 固定变量名

| 变量名 | 文件 | 含义 |
| :--- | :--- | :--- |
| $hoc | Act.Hoc.json | Hoc文件的配置文件，该配置文件中包含了当前组件使用的container的一些固定配置，目的是为了container的重用。 |
| redux | Act.Orbit.js | 当前组件需要使用的redux组件，一般是目录中的顶层UI.js组件和redux连接。 |
| event | Act.Event.js | 当前组件需要使用的JavaScript纯函数。 |
| ui | Act.UI.js | 用于render的一些JSX片段专用函数 |
| Fn | ../../lib/index.js | 工具类 |
| Types | ./Act.Types.js | 当前组件需要使用的Redux的Action信息，一般这个导入在Act.Epic.js中使用 |



