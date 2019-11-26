#### 前言

rem 这个单位对于前端来说并不陌生了,在移动端适配方面,我们经常会用到它,通常我们会采用类似淘宝flexible.js的方案, 写px,然后通过插件转化成rem。

现在已经许多兼容性问题现在不再那么头疼了,因此我们现在有了更好的适配方案（不需要计算插件,不需要写js代码）.

#### 设置meta为移动端

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```

#### 原理

vw表示1%的屏幕宽度,而我们的设计稿通常是750px的,屏幕一共是100vw,对应750px,那么1px就是0.1333333vw；

为了方便计算,我们放大100倍,同时我们知道另一个单位rem,rem是相对html元素,为了方便计算,我们取html是100px,通过上面的计算结果1px是0.13333333vw,那么100px就是13.333333vw了.

这样后面的用rem就很好计算了,这样就得到13.3333333vw对应100px(750px的 设计稿),然后我们就可以很愉快的写rem单位了, 由于倍率是100,我们也不需要啥计算插件之类的了,除以100,直接小数点向左移动2位,1rem是100px,那么10px就是0.1rem,1px就是0.01rem；

不需要用postcss-px-to-viewport这种工具转成一堆小数位特长的rem单位了,而且这个很方便,直接写rem,并不需要转换,用了转换工具 如果想写px的地方还得设置白名单或者黑名单,这个就不存在这种问题了, 想用相对的就rem,想绝对的就直接写px即可,并不需要其他的各种设置。

#### ipad以上的兼容问题

此方案只能兼容手机,甚至连ipad兼容都不好,当然,此处的兼容不是兼容问题,是效果问题,只要兼容vw的设备都能用这个方案,但是由于适配的根本是vw这个, 这个会随着设备的宽度越来越大,那么用rem做单位的元素也会越来越大.

```css
 @media screen and (min-width:560px) {
    html{
        font-size: 54px;
    }
}
```

为什么字体是54px以及为什么是560px为分界线,通过安装flexible.js模拟出来的,flexible.js 在560px以上屏幕就是html{font-size:54px}

完整代码如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        html {
            /* 向下兼容 不止vw时候 写死font-size */
            font-size: 50px; 
            /* 7.5rem === 100vw */
            font-size: 13.33333333vw;
        }
        .app {
            width: 1rem;
            height: 1rem;
            background-color: black;
        }
        p {
            font-size: .28rem;
        }
        span{
            font-size: 28px;
        }

        @media screen and (min-width:560px) {
          html{
            font-size: 54px;
          }
        }

        /* pc*/
        @media screen and (min-width: 999px) {
            html{
                font-size: 100px;
            }
        }

    </style>
</head>

<body>
    <div class="app">

    </div>

    <p>REM</p>
    <span>REM</span>
</body>

</html>

```

#### 扩展

上面那种方式的媒体查询方式是由小到大的方式，如果我们所写的页面包含pc，平板，手机三端，可以采用由大到小的方式书写。代码如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        html {
            font-size: 100px;
        }
        .app {
            width: 1rem;
            height: 1rem;
            background-color: black;
        }
        p {
            font-size: .28rem;
        }
        span{
            font-size: 28px;
        }

         /* 中等屏幕 */
        @media screen and (min-width:992px) and (max-width:1199px) {
          html{

          }
        }

        /* 平板 */
        @media screen and (min-width: 768px) and (max-width: 991px) {
            html {
                font-size: 54px;
            }
        }

        /* 手机*/
        @media screen and (max-width: 767px) {
            html{
                /* 向下兼容 不止vw时候 写死font-size */
                font-size: 50px; 
                /* 7.5rem === 100vw */
                font-size: 13.33333333vw;
            }
        }

    </style>
</head>

<body>
    <div class="app"></div>
    <p>REM</p>
    <span>REM</span>
</body>

</html>
```

#### 参考

[最简单的移动端适配方案(rem+vw)](https://www.jianshu.com/p/5d7779473413)

[三种（rem）移动端适配方案](https://www.jianshu.com/p/268c239002b8)

[移动端布局（封装rem和viewoint两种情况适配）](https://www.jianshu.com/p/9b97e0eb24cd)