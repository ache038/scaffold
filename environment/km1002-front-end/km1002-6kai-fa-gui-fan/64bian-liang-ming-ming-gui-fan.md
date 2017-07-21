# 编码规范

## 1. 基本命名

* 所有子组件名在import的时候第一个字母大写：
  ```js
  import Nav from "./UI.Header";
  ```
* 固定变量参考固定变量命名：[6.3.固定变量名](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/63gu-ding-bian-liang-ming.md)
* 如果变量名来自于资源文件，则使用下划线前缀：`_`
* 如果变量名来自于Redux的stateToProp，则使用美元符号前缀：`$`
* 局部变量命名可自由操作，一般是小写；
* Redux中的数据节点结果一般是data和inited两个，遵循data，dataed的结构（很重要），如：
  ```js
      const $hoteled = state.out['env']['hotel'].inited;
      const $hotel = state.out['env']['hotel'].data;
  ```
* 


