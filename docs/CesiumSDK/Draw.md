# Position

## 加载图标点 loadMarker

- @param

  position : 84坐标

  myData ： 自定义的数据，在监听点击事件时根据此属性获取

  imgUrl ： 图标文件，通过require获取

  imgSize ： 图标大小 默认：{w:40,h:40}

- @returns

  point ： 返回图标点的entity对象。如：

  ```js
  let point = CM.Draw.loadMarker(position, myData, imgUrl);
  ```

## 加载线 loadPolyline

- @param

  position : 线数据

  data ： 自定义的数据，在监听点击事件时根据此属性获取

  LineStyle ：扩展样式，参考cesium文档polygon中的样式配置；使用此对象可替换或增加新的样式。

- @returns

  polyline ： 返回线的entity对象。如：

  ```js
  let polyline = CM.Draw.loadPolyline(position, data, LineStyle);
  ```

## 绘制线 Polyline

- @param

  callback : 返回实体和线数据

  ```js
  CM.Draw.Polyline((polyline, polylineData)=>{});
  ```


## 测量距离 MeasureDistance

- @param

  callback : 返回距离数据

  ```js
  CM.Draw.MeasureDistance((distance)=>{});
  ```

  
## 加载面 loadPolygon

- @param

  position : 面数据

  myData ： 自定义的数据，在监听点击事件时根据此属性获取

  PolygonStyle : 扩展样式，参考cesium文档中的样式配置；使用此对象可替换或增加新的样式。

- @returns

  polygon ： 返回面的entity对象。如：

  ```js
  let polygon = CM.Draw.loadPolygon(position, data, PolygonStyle);
  ```

    
## 加载空心面  loadHollowPolygon

- @param

  position : 面数据

  myData ： 自定义的数据，在监听点击事件时根据此属性获取

  LineStyle : 线的扩展样式，参考cesium文档中的样式配置

  GonStyle : 面扩展样式，参考cesium文档中的样式配置

  LabelStyle : 文本扩展样式，参考cesium文档中的样式配置

- @returns

  polygon ： 返回面的entity对象。如：

  ```js
  let polygon = CM.Draw.loadHollowPolygon(position, data, LineStyle, GonStyle, LabelStyle);
  ```


  
## 绘制面 Polygon

- @param

  callback : 返回实体和面数据

  ```js
  CM.Draw.Polygon((polyline,polygonData)=>{});
  ```


## 测量面积 MeasureArea

- @param

  callback : 返回面积数据

  ```js
  CM.Draw.MeasureArea((area)=>{});
  ```

  
## 加载圆 loadCicle

- @param

  ciclePosition : 圆数据

  myData ： 自定义的数据，在监听点击事件时根据此属性获取

- @returns

  Cicle ： 返回圆的entity对象。如：

  ```js
  let polygon = CM.Draw.loadCicle(ciclePosition, myData);
  ```

## 绘制圆 Cicle

- @param

  callback : 返回圆的entity实体对象和圆数据

  ```js
  CM.Draw.Cicle((cicle,cicleData)=>{});
  ```

## 加载矩形 loadRectangle

- @param

  rectanglePosition : 矩形数据

  myData ： 自定义的数据，在监听点击事件时根据此属性获取

- @returns

  Rectangle ： 返回矩形的entity对象。如：

  ```js
  let rectangle = CM.Draw.loadRectangle(rectanglePosition, myData);
  ```

## 绘制矩形 Rectangle

- @param

  callback : 返回矩形的entity实体对象和矩形数据

  ```js
  CM.Draw.Rectangle((rectangle,rectangleData)=>{});
  ```