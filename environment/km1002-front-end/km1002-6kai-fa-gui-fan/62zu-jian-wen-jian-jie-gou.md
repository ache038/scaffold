# 组件文件结构

## 1. 组件代码结构

1. Import区域，参考：[6.1.Import脚本顺序](/environment/km1002-front-end/km1002-6kai-fa-gui-fan/61importjiao-ben-shun-xu.md)
2. 名称区域，如果需要使用到shared/cn中的资源文件，则该Name变量会作为资源文件专用
3. Component组件定义
4. React构造方法：constructor
5. LifeCycle方法：componentWillMount，componentDidMount等
6. 当前组件内专用方法：以handle为前缀，格式handleXXX这种
7. render方法
8. Prop-Type区域用于检查合法性（合法性在后期加入）
9. 组件displayName赋值语句，对应结构2
10. export部分

## 2. 示例

```javascript
import React from 'react'
// 1.Import区域
import './UI.Steps.less'

import Title from '../text/UI.Title'

import {
    Button, Steps
} from 'antd';

const {
    Step
} = Steps;
// 2.组件名称
const Name = "control.help.Steps";
// 3.组件定义
class Component extends React.PureComponent {
    // 4.构造函数
    constructor(props) {
        super(props);
        const {_default = 0} = props;
        this.state = {current: _default};
    }
    // 6.组件自身方法
    handleNext() {
        const current = this.state['current'] + 1;
        this.setState({current});
    }

    handlePrev() {
        const current = this.state['current'] - 1;
        this.setState({current});
    }

    handleFirst(){
        const { _default = 0 } = this.props;
        this.setState({current:_default})
    }

    handleLast(){
        const { _steps = []} = this.props;
        this.setState({current:_steps.length - 1});
    }
    // 7.render方法
    render() {
        const {_steps = [], _direction = "vertical"} = this.props;
        const {_prev, _next, _first, _last} = this.props;
        const {Fn} = this.props;
        const Lg = Fn.Lg(Name);
        // 可移动的步骤栏
        const {current} = this.state;
        return (
            <dl className="vi-steps">
                <dt>
                    <Title {...Lg}/>
                </dt>
                <dd>
                    <Steps direction={_direction} current={current}>
                        {
                            _steps.map(step => (
                                <Step key={step.key} title={step.title} description={step.info}/>
                            ))
                        }
                    </Steps>
                    {(_prev) ? (<Button id={_prev} className="vi-hidden-btn" onClick={() => {
                        this.handlePrev()
                    }}/>) : false}
                    {(_next) ? (<Button id={_next} className="vi-hidden-btn" onClick={() => {
                        this.handleNext()
                    }}/>) : false}
                    {(_first) ? (<Button id={_first} className="vi-hidden-btn" onClick={() => {
                        this.handleFirst()
                    }}/>) : false}
                    {(_last) ? (<Button id={_last} className="vi-hidden-btn" onClick={() => {
                        this.handleLast()
                    }}/>) : false}
                </dd>
            </dl>
        )
    }
}
// 9.组件displayName赋值
Component.displayName = Name;
// 10.export部分
export default Component
```





