# 全局配置

整个项目的全局配置文件为固定位置：

```json
src/config.json
```

文件结构如下：

```json
{
  "lang":"cn",
  "icon":"ext",
  "endpoint":"http://localhost:8083",
  "name":"vie.app.htl",
  "event":"$$VIE-UI",
  "key":"@@RTV/",
  "debug":true,
  "entry":{
    "login":"/htl/login",
    "admin":"/htl/main/index"
  }
}
```

配置项说明：

| 配置项 | 说明 |
| :--- | :--- |
| lang | 当前资源文件使用的语言信息，该目录会决定资源文件的读取位置：src/shared/cn/xxxx，资源文件位于src/shared中，该文件会被I18nComponent组件根据文件名自动加载——所有使用了该组件的组件必须配置该组件对应资源文件，不可为空！ |
| icon | 当前应用使用的默认图标文件目录，目前使用的目录地址如下：**src/environment/icon/ext**中。 |
| endpoint | 远程访问的Restful专用Endpoint地址【跨域访问】，在Tradeshift平台内部可直接通过相对路径访问，但如果考虑到后期的平台扩展，该配置为应用启动过程需要连接的远程Endpoint Api地址。 |
| name | 当前应用名称，在非数据驱动的结构中不需要该配置，但若是数据驱动则该名称会存储在后端配置中：如后端有一张数据库表为SYS\_APP，对应的应用名字段为S\_NAME，则在部署新的前端应用时，将name作为读取远程配置的依据。 |
| event | Redux专用事件前缀，最终会生成类似下边这种Action名称：$$SCO-UI/SUC/APP/DO/CONFIG，该名称会反应到redux-logger中，不同的应用使用不同的事件前缀 |
| key | Session/Local两种本地存储机制专用的键前缀，最终会在浏览器中生成Key如：@@SCO/SESSION/USER |
| debug | 用于控制Joy中的调试日志，如果该值为true则表示打开日志信息，否则不打开console中的日志信息 |
| entry -&gt; login | 登陆入口页面地址（应用内部页面全部从服务端配置中读） |
| entry -&gt; admin | 登陆过后入口页面 |

\*：entry是临时配置，如果是独立程序则该配置应该从应用程序配置中直接拿到，而不是通过前端配置来读取，后期处理平台多应用架构时再来修订全局配置中的不必要的部分。

