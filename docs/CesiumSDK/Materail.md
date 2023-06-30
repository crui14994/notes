<!--
 * @Author:
 * @Date: 2023-06-30 15:32:17
 * @LastEditTime: 2023-06-30 15:44:38
 * @LastEditors: Please set LastEditors
 * @Description:
-->

# Materail

#### 创建自定义材质 createCustomMaterial

- @param

| 参数名  | type   | 描述                   | 默认值 |
| ------- | ------ | ---------------------- | ------ |
| options | Object | 材质配置，属性参考下表 | -      |

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
let material = CM.Materail.createCustomMaterial(options);
```

###### options 属性

| 属性名    | type   | 描述                     | 默认值 |
| --------- | ------ | ------------------------ | ------ |
| image     | String | 图片地址                 | -      |
| freely    | String | 图片方向(cross/vertical) | -      |
| direction | String | 动画方向 (+/-)           | -      |
| count     | Number | 图片的重复数量           | -      |
| color     | Object | 颜色                     | -      |
| duration  | Number | 动画时长                 | -      |
