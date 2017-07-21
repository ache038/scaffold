# Hoc结构处理

Hoc主要思路如下：

* 让一些特殊容器可重用，直接让子组件传入配置数据；
* 容器本身根据配置读取特殊的一些数据信息；

接下来以Password界面为例，组件连接图如下：

![](/assets/KM1002/008.png)

* 组件内的`UI.js`读取配置数据`Act.Hoc.json`；
* `UI.js`读取数据过后针对数据进行处理（流程不固定，可编程）；
* `UI.js`会连接Redux完成Redux中的一些特殊处理，包括初始化数据并且将数据继承到核心组件；
* 调用特殊方法渲染界面，先渲染容器`control/container/UI.Form.js`（渲染流程固定，逻辑也固定）；
* 最后渲染组件本身`components/user.password/UI.Form.js`；



