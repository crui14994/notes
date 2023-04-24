## Imagery

#### 天地图 createTdtImageryProvider

- @param

| 参数名 | type   | 描述                                           | 默认值 |
| ------ | ------ | ---------------------------------------------- | ------ |
| style  | String | 地图图层类型；可选值（ec、cva、img、cia、ter） | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let img = CM.Imagery.createTdtImageryProvider("img");
let cva = CM.Imagery.createTdtImageryProvider("cva");
viewer.addBaseLayer([img, cva]);
```

#### 百度地图 createBaiduImageryProvider

- @param

| 参数名 | type   | 描述                                           | 默认值 |
| ------ | ------ | ---------------------------------------------- | ------ |
| style  | String | 地图图层类型；可选值（img、vec、normal、dark） | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let img = CM.Imagery.createBaiduImageryProvider("img");
viewer.addBaseLayer([img]);
```

#### 腾讯地图 createTencentImageryProvider

- @param

| 参数名 | type   | 描述                             | 默认值 |
| ------ | ------ | -------------------------------- | ------ |
| style  | String | 地图图层类型；可选值（img,1、4） | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let img = CM.Imagery.createTencentImageryProvider(1);
viewer.addBaseLayer([img]);
```

#### 高德地图 createAmapImageryProvider

- @param

| 参数名 | type   | 描述                                   | 默认值 |
| ------ | ------ | -------------------------------------- | ------ |
| style  | String | 地图图层类型；可选值（img、elec、cva） | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let img = CM.Imagery.createAmapImageryProvider("img");
viewer.addBaseLayer([img]);
```

#### 谷歌地图 createGoogleImageryProvider

- @param

| 参数名 | type   | 描述                                   | 默认值 |
| ------ | ------ | -------------------------------------- | ------ |
| style  | String | 地图图层类型；可选值（img、elec、ter） | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let img = CM.Imagery.createGoogleImageryProvider("img");
viewer.addBaseLayer([img]);
```

#### 创建自定义地图图层 createUrlImageryLayer

- @param

| 参数名  | type   | 描述                                              | 默认值 |
| ------- | ------ | ------------------------------------------------- | ------ |
| options | String | 参考 new Cesium.UrlTemplateImageryProvider 的参数 | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let options ={
  ...
}
let img = CM.Imagery.createUrlImageryLayer(options);
viewer.addBaseLayer([img])
```

#### 创建自定义地形图层 createUrlTerrain

- @param

| 参数名  | type   | 描述                                         | 默认值 |
| ------- | ------ | -------------------------------------------- | ------ |
| options | String | 参考 new Cesium.CesiumTerrainProvider 的参数 | -      |

- @returns

| 返回值   | type   | 描述                                                |
| -------- | ------ | --------------------------------------------------- |
| layerObj | Object | 返回创建的图层对象，通过 Viewer.addBaseLayer 加载。 |

```js
let options ={
  ...
}
let img = CM.Imagery.CesiumTerrainProvider(options);
viewer.addBaseLayer([img])
```

#### 根据 geojson 创建一个地图区域，其它区域已指定颜色填充

- @param

| 参数名  | type   | 描述         | 默认值  |
| ------- | ------ | ------------ | ------- |
| geojson | Object | json 数据    | -       |
| bgColor | String | 填充颜色颜色 | #081122 |

- @returns

| 返回值 | type   | 描述                                            |
| ------ | ------ | ----------------------------------------------- |
| primit | Object | 返回 viewer.scene.primitives.add 创建的图层对象 |

```js
let json = require("******.json");
let primit = CM.Imagery.createGeojsonArea(json);
```
