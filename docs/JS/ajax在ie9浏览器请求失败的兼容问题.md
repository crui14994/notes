#### ajax在ie9浏览器请求失败的兼容问题

在chrome下调试接口的时候都可以正常访问，但是在IE9下访问的时候数据都没有了，查看ajax请求过程，既然没数据，那就是请求失败了，在error的回调里打印信息，确实没进入success回调里;$.ajax方法一直在执行error

#### 针对 拒绝访问 是由于浏览器安全机制导致的，解决方法

为点击IE浏览器的的“工具->Internet 选项->安全->自定义级别”将“其他”选项中的“通过域访问数据源”选中为“启用”或者“提示”，点击确定就可以了（但是此法需要用户自行设置不太现实）

#### 解决办法


1. 解决ajax时出现No Transport，在使用ajax之前添加： **jQuery.support.cors = true**

    ```js
    jQuery.support.cors = true;//浏览器支持跨域访问

    $.ajax({
        url: "http://23y8q85354.qicp.vip/getUserInfo",
        type: "GET",
        dataType: "json",
        async: true,
        cache: false,
        crossDomain:  true == !(document.all),
        success: res => {
            console.log(1,res)
        },
        error: err => {
            console.log(2,err)
        }
    })
    ```

    ##### $.ajax属性及用法

    - async

        默认值: true。默认设置下，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为 false。注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行。

    - cache

        默认值: true，dataType 为 script 和 jsonp 时默认为 false。设置为 false 将不缓存此页面。jQuery 1.2 新功能。

    - IE中的crossDomain=true属性设置

        再ajax请求过程中设置了crossDomain=true属性，再谷歌内核中是可以正确解读为support.cors = true，发现其他浏览器中都是support.cors = true，唯独在IE中support.cors = false，这个属性的判断来自于support.cors = !!xhrSupported && ( "withCredentials" in xhrSupported )，其中xhrSupported= new window.XMLHttpRequest(),ie9中XMLHttpRequest没有withCredentials属性。

2. 在jquery后引入 **[jQuery-ajaxTransport-XDomainRequest](https://github.com/aliabbas-2012/jQuery-ajaxTransport-XDomainRequest)** 插件

    ```html
    <!--[if lte IE 9]>
        <script type='text/javascript' src='//cdnjs.cloudflare.com/ajax/libs/jquery-ajaxtransport-xdomainrequest/1.0.3/jquery.xdomainrequest.min.js'></script>
    <![endif]-->
    ```

#### 如果以上方法不行再试试nginx配置反向代理

```bash

 location /api/ {
    rewrite ^/api/(.*)$ /$1 break;  #所有对后端的请求加一个api前缀方便区分，真正访问的时候移除这个前缀
    # API Server
    proxy_pass http://132.122.14.6:9800/;  #将真正的请求代理到serverB,即真实的服务器地址，ajax的url为/api/user/1的请求将会访问http://www.serverB.com/user/1
}

```

参考：[vue项目部署方式:tomcat部署和nginx部署](https://www.jianshu.com/p/55c0b967e1a4)
