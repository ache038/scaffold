# 编码规范

## 1. 基本规范

* 所有子组件名在import的时候第一个字母大写：
  ```js
  import Nav from "./UI.Header";
  ```
* 固定变量参考固定变量命名：[6.3.固定变量名](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/63gu-ding-bian-liang-ming.md)
* 如果变量名来自于资源文件（I18nComponent），则使用下划线前缀：`_`
* 如果变量名来自于Redux的stateToProp，则使用美元符号前缀：`$`
* environment中的固定全局变量如：`$config, $app, $public, $secure, $oauth`
* 字典序基本规则：为了保证编辑器默认字典序排列，根目录遵循字典序规则
  * 所有的组件全部放到c打头的目录中：`combination, components, container, control`；
  * 所有的全局修改频率小的文件以e打头：`entry, environment, entity`
* JavaScript函数主要包含下边三种：
  * React组件内部函数，使用`handle`前缀，并在构造函数中实现绑定；
  * Redux中的dispatch函数，使用`fn`前缀；
  * JavaScript的生成函数，使用`jf`前缀；
* Session/Storage的前缀以及Action本身的前缀都是直接在`config.json`文件中配置；
* React/AntDesign两个库不在TypeScript导入，也不在vie-joy自己开发的库中导入（这两个导入无法实现按需加载，而且Ant Design本身不支持TypeScript）
* 所有的`entity`中的数据结构使用TypeScript开发，并在脚本中单独导入
* 组件中自己开发的import只有三种：
  * 直接从vie-joy项目中import
  * 从路径`'../../entironment'`中导入，也可使用`'../../environment/index'`
  * 从路径`'../../entity'`中导入，也可使用`'../../entity/index'`
* 禁用vie-joy中的三个主要类：App，OAuth，Premettre，参考下边的禁用原则

## 2. 编码原则

### 2.1. 行为自由原则

行为自由主要针对于Act文件，所有的Act文件（Act.Types、Act.Orbit、Act.Event）可自由导入第三方库、以及其他所有的库信息，且导入顺序不限制，该文件中的所有函数都使用const方式纯函数暴露，不定义任何class，而且Act.Event的书写使用TypeScript，而不是JavaScript：除开Entity中的数据结构以外，只有Event中的纯函数使用TypeScript编写，其他内容还是使用JavaScript编写。

### 2.2. 统一入口原则

每个组件中入口为UI.js文件，且入口中一般包含：Event等核心变量，统一入口需要遵循下边几个规则：

* Event只能从UI.js导入，通过继承的方式往子组件传递，且变量名大写；
* 子组件中严禁导入`Act.Event.ts`；

如下边两个文件：

```js
// 父组件：src/container/main/UI.js
// 导入部分包含

import Event from "./Act.Event";

// ......
// 子组件：src/container/main/UI.Header.js
// 子组件中只能使用属性抽取
componentWillMount() {
    const {Event} = this.props;
    Event.fnNavigator(this.props);
}
```

### 2.3. 资源约定原则

资源文件（特别是语言文件）在当前结构中和组件实现命名规则的绑定，基本命名规则如下：

**组件代码**

```javascript
import {Loch} from 'vie-joy'
import {I18nComponent) from '../../environment'
const Name = 'control.bar.ToolBar';
class Component extends React.PureComponent {
    ...
    render(){
        const { $hoc } = this.props;
        const { ... } = $hoc.to();
    }
}
Component.displayName = Name;
export default I18nComponent(Component,Name,Loch.xxxx);
...
```

资源文件：`src/environment/cn/control/bar.Toolbar.json`

* 文件名和Name中的值一致，其提取方式在render方法中如上；
* 目前应用中的资源文件读取统一使用`I18nComponent`组件来实现，第三参数是vie-joy中的日志方法库，一般用于组件的有：`container, components, form, hoc, control, stateless`
* 使用了Hoc中的`I18nComponent`后，则可直接从属性props中提取变量$hoc，并通过调用$hoc.to\(\)来返回JavaScript专用属性对象：资源文件的key统一使用下划线前缀，`to()`方法调用过后的返回，就是资源文件中的`.json`文件全文。

### 2.4. vie-joy禁用类

禁用类的目的是防止代码的泛滥，主要禁用的类如下：

* App——应用程序专用类
* Premettre——Promise生成类
* OAuth——OAuth认证流程类

上边的类被禁用是防止使用泛滥，真正在使用的时候可通过导入environment/index.js中的全局变量来完成

