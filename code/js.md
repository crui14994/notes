#### 禁止/开启 页面滚动

```js
//禁止页面滚动
$('body').css({ 'position': 'fixed', "width": "100%" });

 //开启页面滚动
$("body").css({ "position": "initial", "height": "auto" });
```

#### 获取滚动距离

```javascript
function ___getPageScroll() {
    var xScroll, yScroll;
    if (self.pageYOffset) {
    yScroll = self.pageYOffset;
    xScroll = self.pageXOffset;
    } else if (document.documentElement && document.documentElement.scrollTop) {
    // Explorer 6 Strict    
    yScroll = document.documentElement.scrollTop;
    xScroll = document.documentElement.scrollLeft;
    } else if (document.body) {// all other Explorers    
    yScroll = document.body.scrollTop;
    xScroll = document.body.scrollLeft;
    }
    arrayPageScroll = new Array(xScroll, yScroll);
    return arrayPageScroll;
};
```

#### 为el1元素绑定事件，点击el1时滚动到el2

```js
 //依赖jQuery
 //el1,el2为元素id
 //如scrollTo("#sBtn01","#sTo01")
 function scrollTo(el1,el2){
    //获得el2元素的位置
    var x =$(el2).offset().top;
    $(el1).on("click",function(){
        $('html,body').animate({
            scrollTop: x-50
        }, 300);
    })
}
```

#### 时间格式化

```js
// 对Date的扩展，将 Date 转化为指定格式的String 
// 月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符， 
// 年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字) 
// 例子： 
// (new Date()).Format("yyyy-MM-dd hh:mm:ss.S") ==> 2015-07-02 08:09:04.423 
// (new Date()).Format("yyyy-M-d h:m:s.S")      ==> 2015-7-2 8:9:4.18 
Date.prototype.Format = function(fmt) 
{ 
var o = { 
    "M+" : this.getMonth()+1,                 //月份 
    "d+" : this.getDate(),                    //日 
    "h+" : this.getHours(),                   //小时 
    "m+" : this.getMinutes(),                 //分 
    "s+" : this.getSeconds(),                 //秒 
    "q+" : Math.floor((this.getMonth()+3)/3), //季度 
    "S"  : this.getMilliseconds()             //毫秒 
  }; 
  if(/(y+)/.test(fmt)) 
    fmt=fmt.replace(RegExp.$1, (this.getFullYear()+"").substr(4 - RegExp.$1.length)); 
  for(var k in o) 
    if(new RegExp("("+ k +")").test(fmt)) 
  fmt = fmt.replace(RegExp.$1, (RegExp.$1.length==1) ? (o[k]) : (("00"+ o[k]).substr((""+ o[k]).length))); 
  return fmt; 
}
```

#### 去数组中重复的元素

```js
//去掉数组中重复的元素(百万数量级)
function unique2(arr){
    //i遍历arr,同时创建两个空数组result和hash
    for(var i=0,result=[],hash=[];
        i<arr.length;
        i++){
        //如果hash中以当前元素为key的元素是undefined
        if(hash[arr[i]]===undefined){
            //将当前元素追加到result结尾
            result[result.length]=arr[i];
            //在hash中添加一个新元素: key为当前元素值,值为true
            hash[arr[i]]=true;
        }
    }//(遍历结束)
    return result;//返回result

}

//生成100个0~1000之间的随机数
for(var i=0,arr=[];i<100;i++){
    arr[i]=Math.floor(Math.random()*1000);
}
console.log(unique2(arr));
//    unique2(arr);
```

#### 使用FileReader实现前端图片预览

```html
<!-- html -->
<input type="file"><br>
<img src="" height="200" alt="Image preview area..." title="preview-img">
```
```js
//js
var fileInput = document.querySelector('input[type=file]');
var previewImg = document.querySelector('img');
fileInput.addEventListener('change', function () {
    var file = this.files[0];
    var reader = new FileReader();
    reader.addEventListener('load', function () {
        previewImg.src = reader.result;
    }, false);
    reader.readAsDataURL(file);
}, false);
```

