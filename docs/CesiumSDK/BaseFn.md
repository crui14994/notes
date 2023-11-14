# BaseFn

#### 空间两点距离计算函数 getSpaceDistance

- @param

| 参数名    | type  | 描述           | 默认值 |
| --------- | ----- | -------------- | ------ |
| positions | Array | 两点的坐标数组 | -      |

- @returns

| 返回值   | type   | 描述       |
| -------- | ------ | ---------- |
| distance | Object | 两点距离。 |

```js
let distance = CM.BaseFn.getSpaceDistance(positions);
```

#### 计算多边形面积 getArea

- @param

| 参数名 | type  | 描述                 | 默认值 |
| ------ | ----- | -------------------- | ------ |
| points | Array | 多边形点位的坐标数组 | -      |

- @returns

| 返回值 | type   | 描述   |
| ------ | ------ | ------ |
| area   | Object | 面积。 |

```js
let area = CM.BaseFn.getArea(points);
```

#### 根据多个坐标点,计算中心点坐标 getPointsCenter

- @param

| 参数名 | type  | 描述           | 默认值 |
| ------ | ----- | -------------- | ------ |
| points | Array | 点位的坐标数组 | -      |

- @returns

| 返回值      | type   | 描述     |
| ----------- | ------ | -------- |
| pointCenter | Object | 中心点。 |

```js
let pointCenter = CM.BaseFn.getPointsCenter(points);
```

#### 使用 canvas 根据图片和文字绘制图片 canvasToImage

- @param

| 参数名    | type   | 描述                                                   | 默认值 |
| --------- | ------ | ------------------------------------------------------ | ------ |
| icon      | String | 图片地址，可以是 url 及 base64 或者 require 引入的图片 | -      |
| text      | String | 图文本内容                                             | -      |
| imgConfig | Object | 其它配置;参考下表                                      | -      |

###### imgConfig 属性

| 属性名      | type   | 描述               | 默认值 |
| ----------- | ------ | ------------------ | ------ |
| iconWidth   | Number | icon 宽度          | 152    |
| iconHeight  | Number | icon 高度          | 152    |
| txtColor    | String | 文本颜色           | #fff   |
| txtFontSize | String | 文本大小           | 16px   |
| txtLeft     | Number | 文本距离左边的位置 |        |
| txtTop      | Number | 文本距离顶部的位置 |        |

- @returns

| 返回值  | type    | 描述             |
| ------- | ------- | ---------------- |
| Promise | Promise | 返回绘制的图片。 |

```js
let icon = require("../**/test.png");
let imgConfig = {
  iconWidth: 112,
  iconHeight: 112,
  txtColor: "#212121",
  txtFontSize: "16px",
};
let pointCenter = CM.BaseFn.canvasToImage(icon, "测试文字", imgConfig);
```
