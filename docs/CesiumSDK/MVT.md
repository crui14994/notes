## MVT

#### 获取所有 MVT 生成的图层 getAllProviderLayers

- @returns

| 返回值      | type  | 描述           | 默认值 |
| ----------- | ----- | -------------- | ------ |
| providerArr | Array | MVT 图层对象。 | -      |

```js
let providerArr = CM.MVT.getAllProviderLayers();
```

#### 加载 MVT 图层 loadMvtLayers

- @param

| 参数名      | type     | 描述                              | 默认值 |
| ----------- | -------- | --------------------------------- | ------ |
| mapboxStyle | Object   | mapbox 的样式配置对象             | -      |
| name        | String   | 指定一个唯一值，用于销毁 MVT 图层 | -      |
| callback    | Function | 加载完成的回调函数                | -      |

- @returns

| 返回值  | type   | 描述                      |
| ------- | ------ | ------------------------- |
| myLayer | Object | 返回当前加载的 MVT 图层。 |

```js
let mapboxStyle = {
  version: 8,
  sources: {
    mvtTest: {
      type: "vector",
      tiles: [`./data/MVT/lakepbf/{z}/{x}/{y}.pbf`],
      minzoom: 4,
      maxzoom: 18,
    },
  },
  layers: [
    {
      id: "polygons",
      source: "mvtTest",
      "source-layer": "lake", //此属性可根据控制台加载的pbf信息中获取，位于preview前几行
      type: "fill",
      paint: {
        // "fill-color": "rgba(19, 129, 187, 1)",
        "fill-color": ["get", "color"], //从属性中取颜色
        "fill-opacity": 0.8,
        "fill-outline-color": "rgba(255, 255, 255, 1)",
      },
    },
  ],
};
CM.MVT.loadMvtLayers(mapboxStyle, "myPBF", (myLayer) => {
  console.log(viewer);
});
```

#### 销毁全部 mvt 图层 destoryMvtAll

在切换加载 MVT 时一定要销毁之前的图层，否则会报错

```js
CM.MVT.destoryMvtAll();
```

#### 根据 name 销毁指定的 mvt 图层 destoryMVT

- @param

| 参数名  | type  | 描述                       | 默认值 |
| ------- | ----- | -------------------------- | ------ |
| nameArr | Array | 字符串数组，要销毁的图层。 | -      |

```js
CM.MVT.destoryMVT(nameArr);
```
