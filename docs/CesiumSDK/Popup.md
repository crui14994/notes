# Imagery

## 创建弹窗 createPopup

- @param

  id : 弹窗id

  wgs_84 : 经纬度坐标 {lng:0, lat:0}

  width : 盒子宽度 默认300

  height : 盒子高度 默认200

  topH : 上下偏移高度
  
  leftW : 左右偏移宽度

```js
CM.Imagery.createPopup(id, wgs_84, width = 300, height = 200, topH = 0, leftW = 0);
```

  
## 关闭popup弹窗 closePopup


  ```js
  CM.Imagery.closePopup();
  ```
