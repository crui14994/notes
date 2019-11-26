## 前端针对ajax请求loading效果实现的方法

#### 一.普通页面实现

>jquery给出了两个函数来判断这两个节点，

判断DOM元素加载完成，还是页面中的所有关联文件（包括图片）

1. $(document).ready()是在页面上所有DOM元素加载完毕后才执行。

2. $(window).load();方法是在网页中所有的元素（包括元素的关联文件）完全加载到浏览器后才执行。

    ```js
    //此处选用load方法
    $(window).load(function(){
        //关闭loading
    });
    ```

#### 二. ajax请求loading效果实现实例：

在页面初始化的时候，在页面body标签的顶部来添加loading层并禁止页面滚动,请求结束后移除loading加载dom元素启用页面滚动。

```js
//依赖jquery
$(document).ajaxStart(function () {
    let str = `
    <div id="loadingBox" tabindex="-1">
        <div class="loading">
            <div class="pswp__preloader__icn">
                <div class="pswp__preloader__cut">
                    <div class="pswp__preloader__donut"></div>
                </div>
            </div>
            <p class="loading-text">正在加载...</p>
        </div>
    </div>
    `;
    $('body *:first').before(str);
    //禁止页面滚动
    $('body').css({ 'position': 'fixed', "width": "100%" });
}).ajaxStop(function () {
    $('#loadingBox').remove();
    //开启页面滚动
    $("body").css({ "position": "initial", "height": "auto" });
})
```

css代码如下：

```css
#loadingBox {
  position: fixed;
  top:0;
  left:0;
  right: 0;
  bottom: 0;
  z-index: 500;
  background-color: rgba(0, 0, 0, 0.75);
  .loading{
    position: absolute;
    top: 45%;
    left: 50%;
    transform: translate(-50%,-50%);
    .loading-text{
      color: #FFF;
      padding: 10px 0;
    }
  }
  .pswp__preloader__icn {
    margin: 0 auto;
    width            : 24px;
    height           : 24px;
    -webkit-animation: clockwise 500ms linear infinite;
    animation        : clockwise 500ms linear infinite;
  }

  .pswp__preloader__cut {
    position: relative;
    width   : 12px;
    height  : 24px;
    overflow: hidden;
    position: absolute;
    top     : 0;
    left    : 0;
  }

  .pswp__preloader__donut {
    box-sizing         : border-box;
    width              : 24px;
    height             : 24px;
    border             : 2px solid #FFF;
    border-radius      : 50%;
    border-left-color  : transparent;
    border-bottom-color: transparent;
    position           : absolute;
    top                : 0;
    left               : 0;
    background         : none;
    margin             : 0;
    -webkit-animation  : donut-rotate 1000ms cubic-bezier(.4, 0, .22, 1) infinite;
    animation          : donut-rotate 1000ms cubic-bezier(.4, 0, .22, 1) infinite;
  }

  @-webkit-keyframes clockwise {
    0% {
      -webkit-transform: rotate(0deg)
    }

    100% {
      -webkit-transform: rotate(360deg)
    }
  }

  @keyframes clockwise {
    0% {
      transform: rotate(0deg)
    }

    100% {
      transform: rotate(360deg)
    }
  }

  @-webkit-keyframes donut-rotate {
    0% {
      -webkit-transform: rotate(0)
    }

    50% {
      -webkit-transform: rotate(-140deg)
    }

    100% {
      -webkit-transform: rotate(0)
    }
  }

  @keyframes donut-rotate {
    0% {
      transform: rotate(0)
    }

    50% {
      transform: rotate(-140deg)
    }

    100% {
      transform: rotate(0)
    }
  }
}
```
