# 状态写

```
StateIn
StateOut
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

* 键值中可包含`.`操作符，会生成对应的状态子树；
* 


