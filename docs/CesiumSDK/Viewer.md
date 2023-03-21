# Viewer

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

## 加载影像图层 addBaseLayer

- @param

  baseLayers(type:Arrary) : 通过 Imagery 创建的图层数组

  removeAllLayer(type:Boolean) ： 是否清除全部图层再加载,默认 false

```js
let img = CM.Imagery.createGoogleImageryProvider("img");
CM.Viewer.addBaseLayer([img]);
```

## 加载地形 addTerrain

- @param

  terrain(type:Object) : 通过new Cesium.CesiumTerrainProvider得到的地形数据

```js
let muchuan = CM.Imagery.createUrlTerrain({ url: "地形url" });
CM.Viewer.addTerrain(muchuan);
```


## 加载kml loadKml

- @param

  kmlUrl(type:String) : kml地址

  fly(type:Boolean) : 是否飞行到kml区域 默认false

```js
CM.Viewer.loadKml("kmlUrl",true);
```

## geoJson loadGeoJson

- @param

  jsonUrl(type:String) : GeoJson地址

  fly(type:Boolean) : 是否飞行到kml区域 默认false

```js
CM.Viewer.loadKml("kmlUrl",true);
```