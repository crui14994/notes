## Viewer

使用步骤

1. 引入 cesiumSdk

```js
import CesiumMap from "../../plugins/CesiumSdk/index.js";
```

2. 初始化地图，并暴露全局变量 CM，viewer; 注意在离开页面时释放全局变量！

```js
let CM = new CesiumMap("cesiumContainer", { imageryProvider: null });
window.CM = CM;
//window.viewer为cesium实例化得到的viewer，与cesiumSDK无关；
// 主要用于cesium本身一些方法的调用和扩展。
window.viewer = CM.Viewer._viewer;
```

#### 设置天空盒 setSkyBox

- @param

| 参数名  | type   | 描述                        | 默认值 |
| ------- | ------ | --------------------------- | ------ |
| sources | Object | 盒子图片组成的 sources 对象 | -      |

```js
let sources = {
  positiveX: "data/images/SkyBox/tycho2t3_80_pxs.jpg",
  negativeX: "data/images/SkyBox/tycho2t3_80_mxs.jpg",
  positiveY: "data/images/SkyBox/tycho2t3_80_pys.jpg",
  negativeY: "data/images/SkyBox/tycho2t3_80_mys.jpg",
  positiveZ: "data/images/SkyBox/tycho2t3_80_pzs.jpg",
  negativeZ: "data/images/SkyBox/tycho2t3_80_mzs.jpg",
};

CM.Viewer.setSkyBox(sources);
```

#### 设置黑夜特效 setDarkEffect

- @returns

| 返回值 | type   | 描述                                |
| ------ | ------ | ----------------------------------- |
| Effect | Object | 返回创建的 postProcessStages 对象。 |

```js
let Effect = CM.Viewer.setDarkEffect();

setTimeout(() => {
  // viewer.postProcessStages.remove(Effect);
  viewer.postProcessStages.removeAll();
}, 5000);
```

#### 设置雨天特效 setSnowEffect

- @returns

| 返回值 | type   | 描述                                |
| ------ | ------ | ----------------------------------- |
| Effect | Object | 返回创建的 postProcessStages 对象。 |

```js
let Effect = CM.Viewer.setSnowEffect();
```

#### 设置雪天特效 setSnowEffect

- @returns

| 返回值 | type   | 描述                                |
| ------ | ------ | ----------------------------------- |
| Effect | Object | 返回创建的 postProcessStages 对象。 |

```js
let Effect = CM.Viewer.setSnowEffect();
```

#### 加载影像图层 addBaseLayer

- @param

| 参数名         | type    | 描述                        | 默认值 |
| -------------- | ------- | --------------------------- | ------ |
| baseLayers     | Arrary  | 通过 Imagery 创建的图层数组 | -      |
| removeAllLayer | Boolean | 是否清除全部图层再加载      | false  |

```js
let img = CM.Imagery.createGoogleImageryProvider("img");
CM.Viewer.addBaseLayer([img]);
```

#### 加载地形 addTerrain

- @param

| 参数名  | type   | 描述                                                 | 默认值 |
| ------- | ------ | ---------------------------------------------------- | ------ |
| terrain | Object | 通过 new Cesium.CesiumTerrainProvider 得到的地形数据 | -      |

```js
let muchuan = CM.Imagery.createUrlTerrain({ url: "地形url" });
CM.Viewer.addTerrain(muchuan);
```

#### 加载 kml loadKml

- @param

| 参数名 | type    | 描述                | 默认值 |
| ------ | ------- | ------------------- | ------ |
| kmlUrl | String  | kml 地址            | -      |
| fly    | Boolean | 是否飞行到 kml 区域 | false  |

```js
CM.Viewer.loadKml("kmlUrl", true);
```

#### geoJson loadGeoJson

- @param

| 参数名   | type     | 描述                          | 默认值 |
| -------- | -------- | ----------------------------- | ------ |
| geoJson  | String   | GeoJson 地址                  | -      |
| myData   | Object   | 自定义数据                    |        |
| callback | Function | 返回数据 entities, dataSource |        |
| style    | Object   | 数据样式                      |        |

```js
CM.Viewer.loadGeoJson(geoJson, {}, (entities, dataSource) => {
  console.log(entities, dataSource)
}, {
  fill: new Cesium.Color.fromCssColorString("rgba(255,255,0,.9)"),
  stroke: new Cesium.Color.fromCssColorString("rgba(255,255,0,1)"), //折线和多边形轮廓的默认颜色
});
```
