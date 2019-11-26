#### 1.video属性

```

<!-- video 不支持 IE8及以下版本浏览器，支持三种视频格式：MP4，WebM 和 Ogg -->
  <video src="test.mp4" controls width="400" height="300"></video>

  <!-- 禁止下载 -->
  <video src="test.mp4" controls controlslist="nodownload" width="400" height="300"></video>

  <!-- 禁止下载，禁止全屏 -->
  <video src="test.mp4" controls controlslist="nodownload nofullscreen" width="400" height="300"></video>

  <!-- 自动播放 （不同浏览器的表现不一样） -->
  <video src="test.mp4" controls autoplay width="400" height="300"></video>

  <!-- 默认静音播放（可手动点开继续播放） -->
  <video src="test.mp4" controls muted width="400" height="300"></video>

  <!-- 循环播放 -->
  <video src="test.mp4" controls loop width="400" height="300"></video>

  <!-- 预加载 -->
  <video src="test.mp4" controls preload width="400" height="300"></video>

  <!-- 贴图 -->
  <video src="test.mp4" poster="poster.jpg" controls width="400" height="300"></video>

  <!-- 音量控制 -->
  <video src="test.mp4" poster="poster.jpg" controls width="400" height="300" id="_volume"></video>
  <script>
    var video = document.getElementById('_volume')
    video.volume = 2 // 取值范围：0 到 1，0 是静音，0.5 是一半的音量，1 是最大音量（默认值）
  </script>

  <!-- 播放时间控制 -->
  <video src="test.mp4" poster="poster.jpg" controls width="400" height="300" id="_time"></video>
  <script>
    var video = document.getElementById('_time')
    console.log(video.currentTime)  // 视频当前正在播放的时间（单位：s），进度条拖到哪就显示当前的时间
    video.currentTime = 60  // 默认从60秒处开始播放
  </script>

  <!-- 播放地址切换 （常见于切换超清  高清 流畅，不同画质的视频地址不同） -->
  <video src="test.mp4" controls autoplay width="400" height="300" id="_src"></video>
  <script>
    var video = document.getElementById('_src')
    console.log(video.src)     // http://127.0.0.1:8001/test.mp4   绝对地址，DOM 中是相对地址
    // video.src = 'test-2.mp4'   // 直接替换掉了原来的视频src
    setTimeout(() => {
      video.src = 'test-2.mp4'  // 播放到第 30s 的时候，自动切换视频
    }, 30000)
  </script>

  <!-- 备用地址切换 -->
  <video controls autoplay width="400" height="300" id="_source">
    <source src="test3.mp4" type="video/mp4" />
    <source src="test9.mp4" type="video/mp4" />
    <source src="test-2.mp4" type="video/mp4" />
  </video>
  <script>
    var video = document.getElementById('_source')
    setTimeout(() => {
      console.log(video.currentSrc)     // http://127.0.0.1:8001/test.mp4
    }, 1000)

    // HTTP 载入失败，状态码 404。媒体资源 http://127.0.0.1:8001/test3.mp4 载入失败。
    // HTTP 载入失败，状态码 404。媒体资源 http://127.0.0.1:8001/test9.mp4 载入失败。
    // http://127.0.0.1:8001/test-2.mp4
    // 当第一段视频加载失败时，自动加载下一段视频

```

#### 2.video 事件

```js
<script>
    var video = document.getElementById('video')

    // 1、loadstart：视频查找。当浏览器开始寻找指定的音频/视频时触发，也就是当加载过程开始时
    video.addEventListener('loadstart', function(e) {
      console.log('提示视频的元数据已加载')
      console.log(e)
      console.log(video.duration)            // NaN
    })

    // 2、durationchange：时长变化。当指定的音频/视频的时长数据发生变化时触发，加载后，时长由 NaN 变为音频/视频的实际时长
    video.addEventListener('durationchange', function(e) {
      console.log('提示视频的时长已改变')
      console.log(e)
      console.log(video.duration)           // 528.981333   视频的实际时长（单位：秒）
    })

    // 3、loadedmetadata ：元数据加载。当指定的音频/视频的元数据已加载时触发，元数据包括：时长、尺寸（仅视频）以及文本轨道
    video.addEventListener('loadedmetadata', function(e) {
      console.log('提示视频的元数据已加载')
      console.log(e)
    })

    // 4、loadeddata：视频下载监听。当当前帧的数据已加载，但没有足够的数据来播放指定音频/视频的下一帧时触发
    video.addEventListener('loadeddata', function(e) {
      console.log('提示当前帧的数据是可用的')
      console.log(e)
    })

    // 5、progress：浏览器下载监听。当浏览器正在下载指定的音频/视频时触发
    video.addEventListener('progress', function(e) {
      console.log('提示视频正在下载中')
      console.log(e)
    })

    // 6、canplay：可播放监听。当浏览器能够开始播放指定的音频/视频时触发
    video.addEventListener('canplay', function(e) {
      console.log('提示该视频已准备好开始播放')
      console.log(e)
    })

    // 7、canplaythrough：可流畅播放。当浏览器预计能够在不停下来进行缓冲的情况下持续播放指定的音频/视频时触发
    video.addEventListener('canplaythrough', function(e) {
      console.log('提示视频能够不停顿地一直播放')
      console.log(e)
    })

    // 8、play：播放监听
    video.addEventListener('play', function(e) {
      console.log('提示该视频正在播放中')
      console.log(e)
    })

    // 9、pause：暂停监听
    video.addEventListener('pause', function(e) {
      console.log('暂停播放')
      console.log(e)
    })

    // 10、seeking：查找开始。当用户开始移动/跳跃到音频/视频中新的位置时触发
    video.addEventListener('seeking', function(e) {
      console.log('开始移动进度条')
      console.log(e)
    })

    // 11、seeked：查找结束。当用户已经移动/跳跃到视频中新的位置时触发
    video.addEventListener('seeked', function(e) {
      console.log('进度条已经移动到了新的位置')
      console.log(e)
    })

    // 12、waiting：视频加载等待。当视频由于需要缓冲下一帧而停止，等待时触发
    video.addEventListener('waiting', function(e) {
      console.log('视频加载等待')
      console.log(e)
    })

    // 13、playing：当视频在已因缓冲而暂停或停止后已就绪时触发
    video.addEventListener('playing', function(e) {
      console.log('playing')
      console.log(e)
    })

    // 14、timeupdate：目前的播放位置已更改时，播放时间更新
    video.addEventListener('timeupdate', function(e) {
      console.log('timeupdate')
      console.log(e)
    })

    // 15、ended：播放结束
    video.addEventListener('ended', function(e) {
      console.log('视频播放完了')
      console.log(e)
    })

    // 16、error：播放错误
    video.addEventListener('error', function(e) {
      console.log('视频出错了')
      console.log(e)
    })

    // 17、volumechange：当音量更改时
    video.addEventListener('volumechange', function(e) {
      console.log('volumechange')
      console.log(e)
    })

    // 18、stalled：当浏览器尝试获取媒体数据，但数据不可用时
    video.addEventListener('stalled', function(e) {
      console.log('stalled')
      console.log(e)
    })

    // 19、ratechange：当视频的播放速度已更改时
    video.addEventListener('ratechange', function(e) {
      console.log('ratechange')
      console.log(e)
    })
</script>

```

#### 3.基本示例

```html
<video id="video" 
  style="object-fit:fill" 
  autoplay
  webkit-playsinline 
  playsinline 
  x5-video-player-type="h5"
  x5-video-player-fullscreen="true"
  x5-video-orientation="portraint" 
  src="video.mp4" />
</video>
<!--
  object-fit: fill   视频内容充满整个video容器
  poster:"img.jpg" 视频封面
  autoplay： 自动播放
     auto - 当页面加载后载入整个视频
     meta - 当页面加载后只载入元数据
     none - 当页面加载后不载入视频

  muted：当设置该属性后，它规定视频的音频输出应该被静音

  webkit-playsinline playsinline:   内联播放

  x5-video-player-type="h5" :  启用x5内核H5播放器（移动端隐藏播放控件）
  x5-video-player-fullscreen="true"  全屏设置。ture和false的设置会导致布局上的不一样
  x5-video-orientation="portraint" ：声明播放器支持的方向，可选值landscape 横屏,portraint竖屏。
                                     默认值portraint。无论是直播还是全屏H5一般都是竖屏播放，
                                     但是这个属性需要x5-video-player-type开启H5模式
-->

```
#### 4.监控下载进度

```js
// 视频时长
var duration = video.duration

// 获取视频已经下载的时长
function getEnd(video) {
  var end = 0
  try {
    end = video.buffered.end(0) || 0
    end = parseInt(end * 1000 + 1) / 1000
  } catch(e) {
  }
  return end
}
```

#### 参考

[h5 video 移动端填坑记](https://www.jianshu.com/p/887e09cb0a10)

[移动端 HTML5 video 视频播放优化实践](https://zhaoda.net/2014/10/30/html5-video-optimization/)

[一款全兼容的播放器 videojs](https://blog.csdn.net/ly115176236/article/details/50977127)