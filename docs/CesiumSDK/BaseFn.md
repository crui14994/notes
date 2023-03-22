# BaseFn

## 空间两点距离计算函数 getSpaceDistance

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

## 计算多边形面积 getArea

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
