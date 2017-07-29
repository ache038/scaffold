# 全局配置

项目名：sco

整个项目的全局配置文件为固定位置：

```json
src/config.json
```

文件结构如下：

```json
{
  "lang":"cn",
  "endpoint":"http://localhost:8083",
  "name":"sco.app.htl",
  "event":"$$SCO-UI",
  "key":"@@SCO/",
  "debug":{
    "ajax":true,
    "form":false,
    "control":true
  },
  "entry":{
    "login":"/sco/login",
    "admin":"/sco/main/index"
  }
}
```

配置项说明：

| 配置项 | 说明 |
| :--- | :--- |
| lang | 当前资源文件使用的语言信息，该目录会决定资源文件的读取位置：src/shared/cn/xxxx，资源文件位于src/shared中，该文件会被I18nComponent组件根据文件名自动加载——所有使用了该组件的组件必须配置该组件对应资源文件，不可为空！ |
| endpoint | 远程访问的Restful专用Endpoint地址【跨域访问】，在Tradeshift平台内部可直接通过相对路径访问，但如果考虑到后期的平台扩展，该配置为应用启动过程需要连接的远程Endpoint Api地址。 |
| name | 当前应用名称，在非数据驱动的结构中不需要该配置，但若是数据驱动则该名称会存储在后端配置中：如后端有一张数据库表为SYS\_APP，对应的应用名字段为S\_NAME，则在部署新的前端应用时，将name作为读取远程配置的依据。 |
| event | Redux专用事件前缀，最终会生成类似下边这种Action名称：$$SCO-UI/SUC/APP/DO/CONFIG，该名称会反应到redux-logger中，不同的应用使用不同的事件前缀 |
| key | Session/Local两种本地存储机制专用的键前缀，最终会在浏览器中生成Key如：@@RTV/SESSION/USER |
| debug -&gt; ajax | 是否开启Ajax调试日志 |
| debug -&gt; form | 是否开启Form调试日志 |
| debug -&gt; control | 是否开启控件级别的调试日志 |
| entry -&gt; login | 登陆入口页面地址（应用内部页面全部从服务端配置中读） |
| entry -&gt; admin | 登陆过后入口页面 |



