## 前端结构

整体项目结构如下：

![](/assets/KM1002/001.png)

整体目录如上图所示，每个目录对应的职能如下：

| 目录 | 简介 | 备注 |
| :--- | :--- | :--- |
| build | Prod发布版目录 | 位于**.gitignore**文件中 |
| config | Webpack配置文件目录 | 【Eject】出来的默认配置文件，目前配置了less-loader处理风格文件。 |
| doc | 文档目录 | Markdown文档专用目录 |
| node\_modules | npm依赖包专用目录 | 位于**.gitignore**文件中 |
| public | 静态资源文件目录 | 存放纯的HTML，CSS，图片等 |
| scripts | 启动脚本目录 | 【Eject】出来的默认启动脚本信息 |
| src/tool | 开发工具包 | 非代码工具，主要用于node环境生成代码，执行命令，检查环境等 |
| src/test | 单元测试包 | 测试用例专用包 |
| src/shared | 共享改动包 | 在添加新模块的过程需要变更的文件包，包含了对应的全局资源配置信息。 |
| src/redux | Redux核心组件包 | Epic和Reducers两种组件专用包 |
| src/lib | 工具包 | 常用的代码工具包 |
| src/entry | 主程序入口 |  |
| src/control | 组件包 | 通用型React组件对应的目录 |
| src/container | 容器组件包 | 常用的模板组件对应目录，一般是HOC |
| src/components | 页面组件包 | 针对特定页面专用目录 |







