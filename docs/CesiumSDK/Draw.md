# Position

## 加载图标点 loadMarker

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
let point = CM.Draw.loadMarker(position, myData, imgUrl);
```

## 加载线 loadPolyline

- @param

| 参数名    | type   | 描述                                                                              | 默认值 |
| --------- | ------ | --------------------------------------------------------------------------------- | ------ |
| position  | Array  | 线数据                                                                            | -      |
| myData    | Object | 自定义的数据，在监听点击事件时根据此属性获取                                      | -      |
| LineStyle | Object | 扩展样式，参考 cesium 文档 polygon 中的样式配置；使用此对象可替换或增加新的样式。 | -      |

- @returns

| 返回值   | type   | 描述                   |
| -------- | ------ | ---------------------- |
| polyline | Object | 返回线的 entity 对象。 |

```js
let polyline = CM.Draw.loadPolyline(position, data, LineStyle);
```

## 绘制线 Polyline

- @param

| 参数名   | type     | 描述                      | 默认值 |
| -------- | -------- | ------------------------- | ------ |
| callback | Function | 回调函数;返回实体和线数据 | -      |

```js
CM.Draw.Polyline((polyline, polylineData) => {});
```

## 测量距离 MeasureDistance

- @param

| 参数名   | type     | 描述                  | 默认值 |
| -------- | -------- | --------------------- | ------ |
| callback | Function | 回调函数;返回距离数据 | -      |

```js
CM.Draw.MeasureDistance((distance) => {});
```

## 加载面 loadPolygon

- @param

| 参数名       | type   | 描述                                                                     | 默认值 |
| ------------ | ------ | ------------------------------------------------------------------------ | ------ |
| position     | Array  | 面数据                                                                   | -      |
| myData       | Object | 自定义的数据，在监听点击事件时根据此属性获取                             | -      |
| PolygonStyle | Object | 扩展样式，参考 cesium 文档中的样式配置；使用此对象可替换或增加新的样式。 | -      |

- @returns

| 返回值  | type   | 描述                   |
| ------- | ------ | ---------------------- |
| polygon | Object | 返回面的 entity 对象。 |

```js
let polygon = CM.Draw.loadPolygon(position, data, PolygonStyle);
```

## 加载空心面 loadHollowPolygon

- @param

| 参数名     | type   | 描述                                         | 默认值 |
| ---------- | ------ | -------------------------------------------- | ------ |
| position   | Array  | 面数据                                       | -      |
| myData     | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -      |
| LineStyle  | Object | 线的扩展样式，参考 cesium 文档中的样式配置   | -      |
| GonStyle   | Object | 面扩展样式，参考 cesium 文档中的样式配置     | -      |
| LabelStyle | Object | 文本扩展样式，参考 cesium 文档中的样式配置   | -      |

- @returns

| 返回值  | type   | 描述                   |
| ------- | ------ | ---------------------- |
| polygon | Object | 返回面的 entity 对象。 |

```js
let polygon = CM.Draw.loadHollowPolygon(
  position,
  data,
  LineStyle,
  GonStyle,
  LabelStyle
);
```

## 绘制面 Polygon

- @param

| 参数名   | type     | 描述                      | 默认值 |
| -------- | -------- | ------------------------- | ------ |
| callback | Function | 回调函数;返回实体和面数据 | -      |

```js
CM.Draw.Polygon((polyline, polygonData) => {});
```

## 测量面积 MeasureArea

- @param

  | 参数名   | type     | 描述         | 默认值 |
  | -------- | -------- | ------------ | ------ |
  | callback | Function | 返回面积数据 | -      |

  ```js
  CM.Draw.MeasureArea((area) => {});
  ```

## 加载圆 loadCicle

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
let Cicle = CM.Draw.loadCicle(ciclePosition, myData);
```

## 绘制圆 Cicle

- @param

| 参数名   | type     | 描述                                      | 默认值 |
| -------- | -------- | ----------------------------------------- | ------ |
| callback | Function | 回调函数;返回圆的 entity 实体对象和圆数据 | -      |

```js
CM.Draw.Cicle((cicle, cicleData) => {});
```

## 加载矩形 loadRectangle

- @param

| 参数名            | type   | 描述                                         | 默认值 |
| ----------------- | ------ | -------------------------------------------- | ------ |
| rectanglePosition | Array  | 矩形数据                                     | -      |
| myData            | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -      |

- @returns

| 返回值    | type   | 描述                     |
| --------- | ------ | ------------------------ |
| Rectangle | Object | 返回矩形的 entity 对象。 |

```js
let rectangle = CM.Draw.loadRectangle(rectanglePosition, myData);
```

## 绘制矩形 Rectangle

- @param

| 参数名   | type     | 描述                                          | 默认值 |
| -------- | -------- | --------------------------------------------- | ------ |
| callback | Function | 回调函数;返回矩形的 entity 实体对象和矩形数据 | -      |

```js
CM.Draw.Rectangle((rectangle, rectangleData) => {});
```
