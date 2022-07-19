
## 业界主流方案

基于 WebView UI 的基础方案，通过 JSBridge（例如微信JS-SDK）完成 H5 与 Native 的双向通信，从而赋予H5一定程度的原生能力。


## 具体实现方式


- 方式1：通过 JSBridge 提供的API方法，分别在App、H5端进行注册和监听，挂在相应的方法。

如果想让App调用H5的方法，或者H5调用App的方法，可以通过方式1。

- 方式2：通过的WebView 的URL Scheme 做跳转。

如果我们想在H5内唤起App，可以用方式2。


## URL Scheme协议

URL Scheme 是一种页面内跳转协议，通过这个协议可以比较方便的跳转到app某一个页面。

URL Scheme格式：

```bash
[scheme]://[host][:port]/[path]?[query]
scheme: 协议名称（由开发人员自定义）(必要，其他都是可选)
host: 域名
port：端口
path: 页面路径
query： 请求参数
```

代码示例：

```js
var userAgent = navigator.userAgent;
var isWeixin = userAgent.toLowerCase().indexOf('micromessenger') !== -1; // 微信内
var isAndroid = /(Android)/i.test(userAgent); //android终端
var isIOS = /(iPhone|iPad|iPod|iOS|Mac|Mac)/i.test(userAgent); //ios终端

// 微信内
if (isWeixin) {
    alert('请在浏览器上打开')
} else {
    //android端
    if (isAndroid) {
        //安卓app的scheme协议
        window.location.href = 'taobao://';
        setTimeout(function () {
           //应用宝下载地址
           window.location.href = "https://a.app.qq.com/o/simple.jsp?pkgname=com.xxx.xxx";
        }, 1000);
    }
    //ios端
    if (isIOS) {
        // 根据时间来判断移动端是否装有app，如果有跳转到和移动端约定好的schema,如果没有装有app则跳转到App Store
        var loadDateTime = Date.now()
        // ios的scheme协议
        window.location.href = 'taobao://'
        //2秒后去App store下载
        setTimeout(function () {
             var timeOutDateTime = Date.now()
             if (timeOutDateTime - loadDateTime < 5000) {
                //App store下载地址
             	window.location.href = "http://itunes.apple.com/app/id387682726";
             }
        }, 2000);
    }
}
```

补充：在浏览器输入 `weixin://`，会唤起微信App。

## 参考链接

- [深入H5与NativeApp通信原理](https://debingfeng.gitee.io/hybrid/%E6%B7%B1%E5%85%A5H5%E4%B8%8ENativeApp%E9%80%9A%E4%BF%A1%E5%8E%9F%E7%90%86.html)

- [通过JsBridge进行app与webview通信（Vue版） ](https://blog.csdn.net/weixin_41891519/article/details/123452727)

- [通过JsBridge进行app与webview通信（Android版）](https://blog.csdn.net/weixin_41891519/article/details/123460959)

- [H5通过URL Scheme协议唤起App](https://blog.csdn.net/weixin_45292658/article/details/108274297)

- [H5唤起APP实践指南 ](https://www.cnblogs.com/GeniusLyzh/p/15235035.html)




