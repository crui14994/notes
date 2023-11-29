<!--
 * @Author:
 * @Date: 2023-06-30 15:32:17
 * @LastEditTime: 2023-11-28 15:24:19
 * @LastEditors: Please set LastEditors
 * @Description:
-->

# Material

#### 创建自定义围墙材质 createWallMaterial

- @param

| 参数名  | type   | 描述                   | 默认值 |
| ------- | ------ | ---------------------- | ------ |
| options | Object | 材质配置，属性参考下表 | -      |

###### options 属性

| 属性名    | type   | 描述                     | 默认值 |
| --------- | ------ | ------------------------ | ------ |
| image     | String | 图片地址                 | -      |
| freely    | String | 图片方向(cross/vertical) | -      |
| direction | String | 动画方向 (+/-)           | -      |
| count     | Number | 图片的重复数量           | -      |
| color     | Object | 颜色                     | -      |
| duration  | Number | 动画时长                 | -      |

- @returns

| 返回值   | type   | 描述   |
| -------- | ------ | ------ |
| material | Object | 材质。 |

```js
let options = {
  image: "data/images/Textures/test1.png",
  freely: "cross",
  direction: "+",
  count: 3,
  color: Cesium.Color.BLUE,
  duration: 2000,
};
let material = CM.Material.createCustomMaterial(options);
```

#### 创建水波纹扩散材质 createCircleWaveMaterial

- @param

| 参数名  | type   | 描述                   | 默认值 |
| ------- | ------ | ---------------------- | ------ |
| options | Object | 材质配置，属性参考下表 | -      |

###### options 属性

| 属性名   | type   | 描述     | 默认值 |
| -------- | ------ | -------- | ------ |
| color    | String | 颜色     | -      |
| speed    | String | 动画速度 | -      |
| count    | Number | 波浪数量 | -      |
| gradient | Number | 渐变曲率 | -      |

- @returns

| 返回值   | type   | 描述   |
| -------- | ------ | ------ |
| material | Object | 材质。 |

```js
let options = {
  color: new Cesium.Color.fromCssColorString("#41A97F"),
  speed: 12.0,
  count: 3,
  gradient: 0.2,
};
let material = CM.Material.createCircleWaveMaterial(options);
```
