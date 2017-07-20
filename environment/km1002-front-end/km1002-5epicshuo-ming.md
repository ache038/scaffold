# Epic说明

Epic负责所有的和后端交互的RxJs模块，其基础目录结构如下：

![](/assets/KM1002/003.png)

## 行为函数

epic目录中的文件为内部纯函数库，每个文件直接开放函数接口，并且不和任何Action相关；真正的Epic对应的Reducer组件在下边两个目录中：

* `ext`：扩展Epic，用于处理新应用的Reducer配置
* `oob`：标准库Epic，Engine专用多个应用可更像的Reducer配置





