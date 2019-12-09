####  jQuery插件编写模板

```js
;(function($,window,document,undefined){

    //定义插件myplugin，在插件中使用MyPlugin对象
    $.fn.videoPlay = function(options){
        return this.each(function() { //保持插件的链式调用，确保插件返回this关键字

            //创建MyPlugin的实体
            var video = new VideoPlay(this,options);
            //调用其方法
            return video.init();

        })

    }

    //定义MyPlugin对象
    var VideoPlay = function(ele,opt){
        this.$element = ele,           //获取到的jQuery对象console.log(this);
        // 设置默认参数
        this.defaults = {

        },
        this.options = $.extend({}, this.defaults, opt);
        //////定义全局变量
        var _this = this,
            navIndex = 0;                                 //当前图片的号数

        //定义私有方法
        //this.auto = function(){
        //    if(_.options.auto===false){
        //        return false;
        //    }
        //    clearInterval(timer);
        //    timer = setInterval(function(){
        //        _.next();
        //    },4000);
        //}
    }


    //定义MyPlugin对象的方法
    VideoPlay.prototype = {
        init:function(){
            //调用私有方法
            //处理DOM
            console.log(0);
        }
    }

})(jQuery,window,document);
```