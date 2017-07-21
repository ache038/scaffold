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

行为自由主要针对于Act文件，所有的Act文件（Act.Types、Act.Orbit、Act.Event、Act.Types）可自由导入第三方库、Fn以及其他所有的库信息，且导入顺序不限制，该文件中的所有函数都使用const方式纯函数暴露，不定义任何class。

### 2.2. 统一入口原则

每个组件中入口为UI.js文件，且入口中一般包含：event、Fn等核心变量（ui变量不放在里面），统一入口需要遵循下边几个规则：

* Fn只能从UI.js导入，通过继承的方式往子组件传递；
* event也只能从UI.js导入，通过继承的方式往子组件传递；
* 子组件一般很干净，import部分只能使用React、第三方库、Less文件、Ant Design组件；

如下边两个文件：

```js
// 父组件：src/container/main/UI.js
// 导入部分包含
import Fn from "../../lib";

import event from "./Act.Event";

// ......
// 子组件：src/container/main/UI.Header.js
// 子组件中只能使用属性抽取
const {Fn = {}, event = {}} = this.props;
```

## 3. 编码技巧

#### State -&gt; Prop

由于继承时通常会涉及到通用属性，所以需要使用以下几个特殊方法来实现统一流程，在State到Prop的过程中，可使用下边的方式抽取节点属性：

```javascript
const mapping = Fn.State.readData(state.out,
        ['app','nav','menu','aside',["hotel","env.hotel"]]);

return {
   ...mapping
}
```

上边代码等价于下边代码

```javascript
const $hotel = state.out.env.hotel.data;
const $hoteled = state.out.env.hotel.inited;
const $app = state.out.app.data;
const $apped = state.out.app.inited;
const $nav = state.out.nav.data;
const $naved = state.out.nav.inited;
const $menu = state.out.menu.data;
const $menued = state.out.menu.inited;
const $aside = state.out.aside.data;
const $asideed = state.out.aside.inited;
return {
    $hotel, $hoteled,
    $app, $apped,
    $nav, $naved,
    $menu, $menued,
    $aside, $asideed
}
```

### Router属性抽取

如果要计算render的渲染条件，尽可能调用下边的代码：

```javascript
const render = Fn.Css.render(this.props, ["app", "nav", "menu", "aside", "hotel"]);
```

上边的代码等价于：

```javascript
const { $apped, $naved, $menued, $asideed, $hoteled } = this.props;
render = $apped && $naved && $menued && $asideed && $hoteled;
```

其含义为：上述的五个变量对应的数据全部加载完成后render才会为true。

