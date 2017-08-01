# 固定变量名

| 变量名 | 文件 | 含义 |
| :--- | :--- | :--- |
| $hoc |  | I18nComponent组件预处理加载的专用资源文件信息，里面所有根节点的Json属性名使用\_前缀 |
| redux | Act.Orbit.js | 当前组件需要使用的redux组件，一般是目录中的顶层UI.js组件和redux连接。 |
| Event | Act.Event.js | 当前组件需要使用的JavaScript纯函数。 |
| ui | Act.UI.js | 用于render的一些JSX片段专用函数 |
| Fn | ../../lib/index.js | 工具类 |
| Types | ./Act.Types.js | 当前组件需要使用的Redux的Action信息，一般这个导入在Act.Epic.js中使用 |
|  | UI.less | 当前组件的专用全局风格文件 |
|  | UI.Auto.less | 当前组件使用的处理响应式变化的less文件，一般是宽度和高度的自适应专用文件 |
| Name | 内部 | 当前组件的名称，有两个用途：一是通过文件名读取对应资源文件；二是直接赋值给displayName用于调试； |
| Lg | 内部 | 一般通过：const Lg = Fn.Lg\(Name\);固定脚本读取，需要使用资源文件时就在render中调用该方法 |



