## 前端结构

整体项目结构如下：

![](/assets/KM1002/001.png)

整体目录如上图所示，每个目录对应的职能如下：

| 目录 | 简介 | 备注 |
| :--- | :--- | :--- |
| build | Prod发布版目录 | 【GitIgnore】生产环境部署目录，编译后的最终信息 |
| config | Webpack配置文件目录 | 【Eject】出来的默认配置文件，目前配置了less-loader处理风格文件，以及TypeScript的脚本环境 |
| node\_modules | npm依赖包专用目录 | 【GitIgnore】依赖库 |
| public | 静态资源文件目录 | 存放纯的HTML，CSS，图片等 |
| scripts | 启动脚本目录 | 【Eject】出来的默认启动脚本信息，启动脚本中引入了生成Epic，Types的专用脚本，执行时会自动生成组件中新添加的Epic和Types文件 |
| src/combination | 高阶组件目录 | High Order Component专用组件 |
| src/components | 页面组件合集 | 对应Router中的page路径组件 |
| src/container | 布局组件合集 | 对应模板Layout组件 |
| src/control | 通用控件合集 | 对应可重用Web组件 |
| src/entity | 前端共享数据模型 | 【TypeScript】主要包含统一的数据结构模型，使用entity命名的目的是保证e打头实现字典序 |
| src/entry | 入口文件集 | 【不变更】store, reducer, epic管理器 |
| src/environment | 环境专用文件 | 当前应用需要使用的共享资源包 |
| src/lang | 语言文件专用包 | 当前应用使用的国际化语言文件资源包 |
| src/tool | 开发工具集 | 生成器 |
| typings | TypeScript依赖 | 【TypeScript】依赖目录 |
| .gitignore |  | GitHub忽略文件配置 |
| package.json |  | npm配置文件 |
| README.md |  | 当前项目说明 |
| refresh-vie-joy.sh |  | vie-joy包更新专用脚本 |
| tsconfig.json |  | typescript配置文件 |
| typings.json |  | typescript依赖库配置 |
| yarn.lock |  | yarn工具配置文件 |

\*：没有枚举出来的内容属于未来将会删除的内容，不包含在项目中，现阶段作用如下：

* \_vie-joy：vie-joy库对应的脚本，用于本地调试；
* lib：原来架构中的工具包，vie-joy的前身，等到项目完全运行后移除；



