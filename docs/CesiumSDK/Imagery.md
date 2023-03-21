# Imagery

## 天地图 createTdtImageryProvider

- @param

  style :vec、cva、img、cia、ter

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let img = CM.Imagery.createTdtImageryProvider("img");
  let cva = CM.Imagery.createTdtImageryProvider("cva");
  viewer.addBaseLayer([img, cva]);
  ```

## 百度地图 createBaiduImageryProvider

- @param

  style :img、vec、normal、dark

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let img = CM.Imagery.createBaiduImageryProvider("img");
  viewer.addBaseLayer([img]);
  ```

## 腾讯地图 createTencentImageryProvider

- @param

  style :img,1、4

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let img = CM.Imagery.createTencentImageryProvider(1);
  viewer.addBaseLayer([img]);
  ```

## 高德地图 createAmapImageryProvider

- @param

  style :img、elec、cva

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let img = CM.Imagery.createAmapImageryProvider("img");
  viewer.addBaseLayer([img]);
  ```

  ## 谷歌地图 createGoogleImageryProvider

- @param

  style :img、elec、ter

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let img = CM.Imagery.createGoogleImageryProvider("img");
  viewer.addBaseLayer([img]);
  ```

## 创建自定义地图图层 createUrlImageryLayer

- @param

  options :参考 new Cesium.UrlTemplateImageryProvider 的参数

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let options ={
    ...
  }
  let img = CM.Imagery.createUrlImageryLayer(options);
  viewer.addBaseLayer([img])
  ```

  ## 创建自定义地形图层 createUrlTerrain

- @param

  options :参考 new Cesium.CesiumTerrainProvider 的参数

- @returns

  返回创建的图层对象，通过 Viewer.addBaseLayer 加载。如：

  ```js
  let options ={
    ...
  }
  let img = CM.Imagery.CesiumTerrainProvider(options);
  viewer.addBaseLayer([img])
  ```
