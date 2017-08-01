# 编码规范

## 1. 基本规范

* 所有子组件名在import的时候第一个字母大写：
  ```js
  import Nav from "./UI.Header";
  ```
* 固定变量参考固定变量命名：[6.3.固定变量名](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/63gu-ding-bian-liang-ming.md)
* 如果变量名来自于资源文件（I18nComponent），则使用下划线前缀：`_`
* 如果变量名来自于Redux的stateToProp，则使用美元符号前缀：`$`
* 
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

### 2.3. 资源约定原则

资源文件（特别是语言文件）在当前结构中和组件实现命名规则的绑定，基本命名规则如下：

**组件代码**

```javascript
const Name = 'control.bar.ToolBar';
class Component extends React.PureComponent {
    ...
    render(){
        ...
        const Lg = Fn.Lg(Name);
        ...
    }
}
Component.displayName = Name;
...
```

资源文件：`src/shared/cn/control.bar.Toolbar.json`

\*：文件名和Name中的值一致，其提取方式在render方法中如上。

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

如果要将Router中的属性继承，那么可以使用下边的方式将React Router中的属性从父组件继承到子组件：

```jsx
<User {...facade}
      {...Fn.Prop.router(this.props)}
      {...Fn.Prop.get(this.props, ['app'])}/>
```

注意上边的`Fn.Prop.router(this.props)`，这是抽取react-router中的属性，其内部实现如下：

```javascript
const router = (props = {}) => {
    // 提取React Router属性专用
    const { history, location, match } = props;
    return { history, location, match }
};
```

上边的代码等价于：

```jsx
<User history={history} location={location} match={match}/>
```

### 数据属性抽取

回到上边例子中的`Fn.Prop.get(this.props, ['app'])`代码，给个更复杂的：

```jsx
<Menu {...facade} {...$page}
        {...Fn.Prop.get(this.props, ['app', 'aside', 'menu'])}/>
```

除开上边的facade和page过后的等价代码如下：

```jsx
<Menu $app={$app} $apped={$apped} 
        $aside={$aside} $asideed={$asideed} 
        $menu={$menu} $menued={$menued}/>
```

从Menu中可以看到如下：

