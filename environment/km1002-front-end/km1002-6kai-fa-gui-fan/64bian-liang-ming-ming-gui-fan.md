# 编码规范

## 1. 基本规范

* 所有子组件名在import的时候第一个字母大写：
  ```js
  import Nav from "./UI.Header";
  ```
* 固定变量参考固定变量命名：[6.3.固定变量名](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/63gu-ding-bian-liang-ming.md)
* 如果变量名来自于资源文件，则使用下划线前缀：`_`
* 如果变量名来自于Redux的stateToProp，则使用美元符号前缀：`$`
* 自己用的函数分为三种：
  * React内部函数：`handle`前缀
  * Event中的生成函数：`js`前缀
  * Event中的直接调用函数或Dispatch、Reducer函数：`fn`前缀
* 局部变量命名可自由操作，一般是小写；
* Redux中的数据节点结果一般是data和inited两个，遵循data，dataed的结构（很重要），如：
  ```js
  const $hoteled = state.out['env']['hotel'].inited;
  const $hotel = state.out['env']['hotel'].data;
  ```
* 资源文件位于shared/cn/目录下，一般是json格式，其文件名需要和组件中的Name一致，才能被读取，读取的代码一般是固定的：
  ```js
  const Lg = Fn.Lg
  ```
* `Act.Orbit`中的规范统一如下：
  * State -&gt; Prop：命名为`indexS2P`
  * Dispatch -&gt; Prop：命名为`indexD2P`
  * export的函数名为：`connectUI`
* `Act.Event`中一般包含两种JavaScript函数：
  * 以js为前缀的函数：生成函数，调用一次过后生成JavaScript函数
  * 以fn为前缀的函数，直接调用函数，遵循函数命名基本规范
* 所有的Action名称前缀：`<event>/SUC/`
* 所有的Session/Local的存储键名前缀：`<key>`

## 2. 编码原则

### 2.1. 行为自由原则



