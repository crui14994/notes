## Draw

#### 加载图标点 loadMarker

- @param

| 参数名   | type   | 描述                                         | 默认值      |
| -------- | ------ | -------------------------------------------- | ----------- |
| position | Object | 84 坐标                                      | -           |
| myData   | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -           |
| imgUrl   | Object | 图标文件，通过 require 获取                  | -           |
| imgSize  | Object | 图标大小                                     | {w:40,h:40} |

- @returns

| 返回值 | type   | 描述                       |
| ------ | ------ | -------------------------- |
| point  | Object | 返回图标点的 entity 对象。 |

```js
let position = {
  lng: "104.706527",
  lat: "31.448707",
  height: 0,
};
let point = CM.Draw.loadMarker(position, myData, imgUrl);
```

#### 加载线 loadPolyline

- @param

| 参数名    | type   | 描述                                                                              | 默认值 |
| --------- | ------ | --------------------------------------------------------------------------------- | ------ |
| position  | Array  | 线数据，世界坐标数组                                                              | -      |
| myData    | Object | 自定义的数据，在监听点击事件时根据此属性获取                                      | -      |
| LineStyle | Object | 扩展样式，参考 cesium 文档 polygon 中的样式配置；使用此对象可替换或增加新的样式。 | -      |

- @returns

| 返回值   | type   | 描述                   |
| -------- | ------ | ---------------------- |
| polyline | Object | 返回线的 entity 对象。 |

```js
let positionWgs84 = [
  { lng: 104.55, lat: 30.66 },
  { lng: 104.65, lat: 30.56 },
  { lng: 104.75, lat: 30.46 },
  { lng: 104.85, lat: 30.36 },
];
//84坐标转世界坐标
let cartesianArr =
  CM.Position.transformWGS84ArrayToCartesianArray(positionWgs84);

let polyline = CM.Draw.loadPolyline(cartesianArr, data, LineStyle);
```

#### 绘制线 Polyline

- @param

| 参数名    | type     | 描述                                                                               | 默认值 |
| --------- | -------- | ---------------------------------------------------------------------------------- | ------ |
| callback  | Function | 回调函数;返回实体和线数据(84 坐标)                                                 | -      |
| measure   | Boolean  | 是否是测量                                                                         | -      |
| LineStyle | Object   | 扩展样式，参考 cesium 文档 polyline 中的样式配置；使用此对象可替换或增加新的样式。 | -      |

```js
CM.Draw.Polyline((polyline, polylineData) => {});
```

#### 测量距离 MeasureDistance

- @param

| 参数名   | type     | 描述                  | 默认值 |
| -------- | -------- | --------------------- | ------ |
| callback | Function | 回调函数;返回距离数据 | -      |

```js
CM.Draw.MeasureDistance((distance) => {});
```

#### 加载面 loadPolygon

- @param

| 参数名       | type   | 描述                                                                     | 默认值 |
| ------------ | ------ | ------------------------------------------------------------------------ | ------ |
| position     | Array  | 面数据 ，世界坐标数组                                                    | -      |
| myData       | Object | 自定义的数据，在监听点击事件时根据此属性获取                             | -      |
| PolygonStyle | Object | 扩展样式，参考 cesium 文档中的样式配置；使用此对象可替换或增加新的样式。 | -      |

- @returns

| 返回值  | type   | 描述                   |
| ------- | ------ | ---------------------- |
| polygon | Object | 返回面的 entity 对象。 |

```js
let positionWgs84 = [
  { lng: 104.55, lat: 30.66 },
  { lng: 106.65, lat: 31.56 },
  { lng: 107.75, lat: 32.46 },
  { lng: 108.85, lat: 33.36 },
];
//84坐标转世界坐标
let cartesianArr =
  CM.Position.transformWGS84ArrayToCartesianArray(positionWgs84);
let polygon = CM.Draw.loadPolygon(cartesianArr, data, PolygonStyle);
```

#### 绘制面 Polygon

- @param

| 参数名       | type     | 描述                                                                              | 默认值 |
| ------------ | -------- | --------------------------------------------------------------------------------- | ------ |
| callback     | Function | 回调函数;返回实体和面数据(84 坐标)                                                | -      |
| measure      | Boolean  | 是否是测量                                                                        | -      |
| PolygonStyle | Object   | 扩展样式，参考 cesium 文档中 Polygon 的样式配置；使用此对象可替换或增加新的样式。 | -      |

```js
CM.Draw.Polygon((polyline, polygonData) => {});
```

#### 加载带边框的面（空心面） loadHollowPolygon

- @param

| 参数名     | type   | 描述                                         | 默认值 |
| ---------- | ------ | -------------------------------------------- | ------ |
| position   | Array  | 面数据,世界坐标数组                          | -      |
| myData     | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -      |
| LineStyle  | Object | 线的扩展样式，参考 cesium 文档中的样式配置   | -      |
| GonStyle   | Object | 面扩展样式，参考 cesium 文档中的样式配置     | -      |
| LabelStyle | Object | 文本扩展样式，参考 cesium 文档中的样式配置   | -      |

- @returns

| 返回值  | type   | 描述                   |
| ------- | ------ | ---------------------- |
| polygon | Object | 返回面的 entity 对象。 |

```js
let positionWgs84 = [
  { lng: 104.55, lat: 30.66 },
  { lng: 104.65, lat: 30.56 },
  { lng: 104.75, lat: 30.46 },
  { lng: 104.85, lat: 30.36 },
];
//84坐标转世界坐标
let cartesianArr =
  CM.Position.transformWGS84ArrayToCartesianArray(positionWgs84);

let polygon = CM.Draw.loadHollowPolygon(
  cartesianArr,
  data,
  LineStyle,
  GonStyle,
  LabelStyle
);
```

#### 绘制带边框的面（空心面） HollowPolygon

- @param

| 参数名     | type     | 描述                                       | 默认值 |
| ---------- | -------- | ------------------------------------------ | ------ |
| callback   | Function | 回调函数;返回实体和面数据(84 坐标)         | -      |
| LineStyle  | Object   | 线的扩展样式，参考 cesium 文档中的样式配置 | -      |
| GonStyle   | Object   | 面扩展样式，参考 cesium 文档中的样式配置   | -      |
| LabelStyle | Object   | 文本扩展样式，参考 cesium 文档中的样式配置 | -      |

```js
let LineStyle = {
  width: 3,
  material: new Cesium.Color.fromCssColorString("#fff"),
};
let GonStyle = {
  material: new Cesium.Color.fromCssColorString("#fff").withAlpha(0.5),
};
CM.Draw.HollowPolygon(
  (hollowPolygon, polygonData) => {
    console.log(hollowPolygon);
    console.log(polygonData);
  },
  LineStyle,
  GonStyle
);
```

#### 加载圆 loadCicle

- @param

| 参数名        | type   | 描述                                         | 默认值 |
| ------------- | ------ | -------------------------------------------- | ------ |
| ciclePosition | Array  | 圆数据                                       | -      |
| myData        | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -      |

- @returns

| 返回值 | type   | 描述                   |
| ------ | ------ | ---------------------- |
| Cicle  | Object | 返回圆的 entity 对象。 |

```js
let positionWgs84 = [
  { lng: 104.69567372813435, lat: 31.450207195284513, height: 0 },
  { lng: 104.70273793520899, lat: 31.444257890981987, height: 0 },
];
//84坐标转世界坐标
let cartesianArr =
  CM.Position.transformWGS84ArrayToCartesianArray(positionWgs84);

let Cicle = CM.Draw.loadCicle(cartesianArr, myData);
```

#### 绘制圆 Cicle

- @param

| 参数名   | type     | 描述                                      | 默认值 |
| -------- | -------- | ----------------------------------------- | ------ |
| callback | Function | 回调函数;返回圆的 entity 实体对象和圆数据 | -      |

```js
CM.Draw.Cicle((cicle, cicleData) => {});
```

#### 加载矩形 loadRectangle

- @param

| 参数名            | type   | 描述                                         | 默认值 |
| ----------------- | ------ | -------------------------------------------- | ------ |
| rectanglePosition | Array  | 矩形数据 ,世界坐标数组                       | -      |
| myData            | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -      |

- @returns

| 返回值    | type   | 描述                     |
| --------- | ------ | ------------------------ |
| Rectangle | Object | 返回矩形的 entity 对象。 |

```js
let positionWgs84 = [
  { lng: 104.6926049397171, lat: 31.449924438393886, height: 0 },
  { lng: 104.70397349861078, lat: 31.444611031898347, height: 0 },
];
//84坐标转世界坐标
let cartesianArr =
  CM.Position.transformWGS84ArrayToCartesianArray(positionWgs84);

let rectangle = CM.Draw.loadRectangle(cartesianArr, myData);
```

#### 绘制矩形 Rectangle

- @param

| 参数名   | type     | 描述                                                   | 默认值 |
| -------- | -------- | ------------------------------------------------------ | ------ |
| callback | Function | 回调函数;返回矩形的 entity 实体对象和矩形数据(84 坐标) | -      |

```js
CM.Draw.Rectangle((rectangle, rectangleData) => {});
```

#### 创建一个带材质的墙体 loadWall

- @param

| 参数名       | type   | 描述                                                        | 默认值 |
| ------------ | ------ | ----------------------------------------------------------- | ------ |
| wallPosition | Array  | 带高度的经纬度数组 如：[103.56,30.2,500,104.2,31.6,500,...] | -      |
| material     | Object | 材质；根据 CM.Materail.createCustomMaterial 方法创建        | -      |
| wallStyle    | Object | 其它一些关于 wall 的配置，参考 cesium 官方文档              | -      |

- @returns

| 返回值     | type   | 描述                     |
| ---------- | ------ | ------------------------ |
| wallEntity | Object | 返回一个 wall 实体对象。 |

```js
let wallPosition = [
  104.07263175401185, 30.647622150198725, 500.0, 104.06369117158526,
  30.648834374000277, 500.0, 104.06437182811021, 30.62274533905387, 500.0,
  104.07463538167119, 30.62285687644371, 500.0, 104.07263175401185,
  30.647622150198725, 500.0,
];
let material = CM.Material.createCustomMaterial({
  image: "data/images/Textures/test1.png",
  freely: "cross",
  direction: "+",
  count: 3,
  color: Cesium.Color.BLUE,
  duration: 2000,
});

let wallEntity = CM.Draw.loadWall(wallPosition, material);
```

#### 创建一个水波纹图标点 loadCircleWaveMarker

- @param

| 参数名  | type   | 描述                           | 默认值 |
| ------- | ------ | ------------------------------ | ------ |
| options | Object | 水波纹图标点配置，属性参考下表 | -      |

###### options 属性

| 属性名       | type   | 描述                                                     | 默认值                                      |
| ------------ | ------ | -------------------------------------------------------- | ------------------------------------------- |
| position     | Object | 84 坐标                                                  | -                                           |
| material     | Object | 材质；根据 CM.Materail.createCircleWaveMaterial 方法创建 | -                                           |
| ellipseStyle | Object | 其它一些关于 ellipse 的配置，参考 cesium 官方文档        | { semiMinorAxis: 2000,semiMajorAxis: 2000,} |
| myData       | Object | 自定义的数据，在监听点击事件时根据此属性获取             | -                                           |
| imgUrl       | Object | 图标文件，通过 require 获取                              | -                                           |
| imgSize      | Object | 图标大小                                                 | {w:40,h:40}                                 |

- @returns

| 返回值           | type   | 描述                           |
| ---------------- | ------ | ------------------------------ |
| circleWaveEntity | Object | 返回一个 circleWave 实体对象。 |

```js
let material = CM.Material.createCircleWaveMaterial({
  color: new Cesium.Color.fromCssColorString("#41A97F"),
  speed: 12.0,
  count: 3,
  gradient: 0.2,
});

let circleWaveEntity = CM.Draw.loadCircleWaveMarker({
  position: { lng: "105.885597", lat: "32.67532" },
  material,
  // ellipseStyle: {
  //   semiMinorAxis: 2000,
  //   semiMajorAxis: 2000,
  // },
  // imgUrl:'',
  // myData:{},
  // imgSize:{ w: 40, h: 40 }
});
```

#### 编辑 entity(线、面)对象 startEditEntity

- @param

| 参数名   | type   | 描述                                                     | 默认值 |
| -------- | ------ | -------------------------------------------------------- | ------ |
| entity   | Object | entity 对象                                              | -      |
| callback | Array  | 回调函数，每次拖动一个点后鼠标弹起触发，返回一个坐标数组 | -      |

```js
CM.Draw.startEditEntity(entity, (positions) => {
  console.log(positions);
});
```

#### 停止编辑 entity 对象

- @param

| 参数名   | type  | 描述                                 | 默认值 |
| -------- | ----- | ------------------------------------ | ------ |
| callback | Array | 回调函数，返回当前编辑的 entity 对象 | -      |

```js
CM.Draw.stopEditEntity((res) => {
  console.log(res);
});
```

#### 测量面积 MeasureArea

- @param

  | 参数名   | type     | 描述         | 默认值 |
  | -------- | -------- | ------------ | ------ |
  | callback | Function | 返回面积数据 | -      |

  ```js
  CM.Draw.MeasureArea((area) => {});
  ```
