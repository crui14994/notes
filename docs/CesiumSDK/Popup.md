## Imagery

#### 创建弹窗 createPopup

- @param

| 参数名 | type   | 描述                      | 默认值 |
| ------ | ------ | ------------------------- | ------ |
| id     | String | 弹窗 id                   | -      |
| wgs_84 | Object | 经纬度坐标 {lng:0, lat:0} | -      |
| width  | String | 盒子宽度                  | 300    |
| height | String | 盒子高度                  | 200    |
| topH   | String | 上下偏移高度              | -      |
| leftW  | String | 左右偏移宽度              | -      |

```js
CM.Imagery.createPopup(
  id,
  wgs_84,
  (width = 300),
  (height = 200),
  (topH = 0),
  (leftW = 0)
);
```

#### 关闭 popup 弹窗 closePopup

```js
CM.Imagery.closePopup();
```
