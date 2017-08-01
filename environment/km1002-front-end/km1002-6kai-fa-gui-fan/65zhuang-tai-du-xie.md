# 状态写

```
StateIn
```

## 1.写状态

所有的Redux状态树使用StateIn统一写入，调用脚本如下边片段：

```javascript
            return Taper.fnFlush(DataLabor.createIn(
                {
                    "app":app,
                    "layout.nav":processed.nav,
                    "layout.menu":processed.menu,
                    "layout.aside":processed.sidebar
                },
                (payload = {}) => {
                    $app.write(payload['app'].get());
                }
            ));
```

直接在fnFlush函数中传入一个StateIn对象，该对象包含两个核心参数：

* 数据的mapping
* callback处理函数

Mapping的规则如下：

* 键值中可包含`.`操作符，会生成对应的状态子树，如上图：`layout.nav`会直接挂在`out.layout.nav`节点上；
* 写入的数据类型包含三种
  * DataContainer：直接写入，不进行任何转换
  * Object：构造一个DataObject写入
  * Array：构造一个DataArray写入
* callback函数会在最终返回状态之前进行操作，但不更新状态本身！切记。

## 2.纯状态写入

（开发中）



