# 全局配置

整个项目的全局配置文件为固定位置：

```json
src/config.json
```

文件内容如下：

```json
{
  "lang":"cn",
  "endpoint":"http://localhost:8083",
  "name":"vie.app.htl",
  "event":"$$VIE-UI",
  "key":"@@RTV/",
  "debug":{
    "ajax":true,
    "form":false,
    "control":true
  },
  "entry":{
    "login":"/htl/login",
    "admin":"/htl/main/index"
  }
}
```

配置项说明：

| 配置项 | 说明 |
| :--- | :--- |
| lang | 当前资源文件使用的语言信息，该目录会决定资源文件的读取位置：src/shared/cn/xxxx，资源文件位于src/shared中 |
| endpoint | 远程访问的Restful专用Endpoint地址【跨域访问】 |
| name | 当前应用名称，该名称需要和后端SYS\_APP表中的S\_NAME字段对应，应用启动页会从后端读取该应用更加细节的全局配置信息。 |
| event | Redux专用事件前缀，最终会生成类似下边这种Action名称：$$VIE-UI/SUC/APP/DO/CONFIG，该名称会反应到redux-logger中 |
| key | Session/Local两种本地存储机制专用的键前缀，最终会在浏览器中生成Key如：@@RTV/SESSION/USER |
| debug -&gt; ajax | 是否开启Ajax调试日志 |
| debug -&gt; form | 是否开启Form调试日志 |
| entry -&gt; login | 登陆入口页面地址（应用内部页面全部从服务端配置中读） |
| entry -&gt; admin | 登陆过后入口页面 |



