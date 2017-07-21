# ToolBar

## 1. 截图

![](/assets/KM1002/006.png)

## 2. 属性props

![](/assets/KM1006/007.png)

## 3. 备注

* $connect属性中会包含键值对应的函数信息，一般函数会在最初的Hoc配置中转换成函数，如上图最初的Hoc配置为：
  ```json
    "bar":{
      "left":[
        "save",
        "reset"
      ],
      "right":[
        "question"
      ]
    },
    "connect":{
      "save":"btnSave",
      "reset":"btnReset"
    }
  ```
* save和reset中的函数生成代码如下：

  ```js
  // 抽取重要的几个协变函数，用于直接点击过后的前期绑定
  const connect = Fn.Op.bind($hoc.connect);

  // 函数绑定操作，用于触发virtual button -> real button的连接操作
  const bind = (connect = {}) => {
      const result = {};
      for(const key in connect){
          const id = connect[key];
          result[key] = () => {
              click(id);
          };
      }
      return result;
  };
  ```

* hoc中的left、right的配置会影响按钮的效果：
  * left中的按钮效果以：显示/不显示
  * right中的按钮效果以：禁用/不禁用为主



