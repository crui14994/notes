## Position

#### 获取相机位置及姿态 getCameraAttitude

- @returns

| 返回值    | type   | 描述                 |
| --------- | ------ | -------------------- |
| cameraObj | Object | 返回相机位置及姿态。 |

```js
let res = CM.Position.getCameraAttitude();
```

#### 根据屏幕坐标 获取世界坐标、地形坐标、场景坐标 getClickPosition

- @param

| 参数名        | type   | 描述                                                      | 默认值 |
| ------------- | ------ | --------------------------------------------------------- | ------ |
| eventPosition | Object | event.position                                            |        |
| type          | String | 1-世界坐标（地图/椭球体表面的坐标） 2-地形坐标 3-场景坐标 | 1      |

- @returns

| 返回值      | type   | 描述                 |
| ----------- | ------ | -------------------- |
| positionObj | Object | 返回指定类型的坐标。 |

```js
//当前点击视线与椭球面相交处的坐标
let position1 = CM.Position.getClickPosition(eventPosition, 1);

//只能求交于地形，不包括模型、倾斜摄影表面，能获取加载地形后的坐标，pick(ray, scene, result) → Cartesian3|undefined
let position2 = CM.Position.getClickPosition(eventPosition, 2);

//根据窗口坐标，从场景的深度缓冲区中拾取相应的位置，返回笛卡尔坐标，不仅可以求交地形，还可以求交除地形以外其他所有写深度的物体。pickPosition(windowPosition, result) → Cartesian3
let position3 = CM.Position.getClickPosition(eventPosition, 3);
```

#### 根据经纬度获取 terrain 高程，精度为 m getHeigthByLonLat

- @param

| 参数名 | type   | 描述 | 默认值 |
| ------ | ------ | ---- | ------ |
| lng    | String | 经度 | -      |
| lat    | String | 纬度 | -      |

- @returns

| 返回值     | type   | 描述                                          |
| ---------- | ------ | --------------------------------------------- |
| PromiseObj | Object | 返回一个 Promise 对象；并在 then 中返回高度。 |

```js
CM.Position.getHeigthByLonLat("35.125", "104.5").then((height) => {
  console.log(height);
});
```

#### 世界坐标转换为 84 坐标(纬度坐标) transformCartesianToWGS84

- @param

| 参数名    | type   | 描述               | 默认值 |
| --------- | ------ | ------------------ | ------ |
| cartesian | Object | cartesian 世界坐标 | -      |

- @returns

| 返回值   | type   | 描述                           |
| -------- | ------ | ------------------------------ |
| wgs84Obj | Object | 返回一个经纬度高度的 84 坐标。 |

```js
let wgs84 = CM.Position.transformCartesianToWGS84(cartesian);
```

#### 84 坐标(纬度坐标)转换为世界坐标 transformWGS84ToCartesian

- @param

| 参数名   | type   | 描述                 | 默认值 |
| -------- | ------ | -------------------- | ------ |
| position | Object | 经纬度高度的 84 坐标 | -      |

- @returns

| 返回值        | type   | 描述                           |
| ------------- | ------ | ------------------------------ |
| Cartesian3Obj | Object | 返回一个 Cartesian3 世界坐标。 |

```js
let wgs84 = { lng: 104.6926049397171, lat: 31.449924438393886, height: 0 };
let wgs84 = CM.Position.transformWGS84ToCartesian(wgs84);
```

#### 84 纬度坐标转换为 84 弧度坐标 transformWGS84ToCartographic

- @param

| 参数名   | type   | 描述                 | 默认值 |
| -------- | ------ | -------------------- | ------ |
| position | Object | 经纬度高度的 84 坐标 | -      |

- @returns

| 返回值          | type   | 描述                                |
| --------------- | ------ | ----------------------------------- |
| CartographicObj | Object | 返回一个 cartographic 84 弧度坐标。 |

```js
let wgs84 = { lng: 104.6926049397171, lat: 31.449924438393886, height: 0 };
let cartographic = CM.Position.transformWGS84ToCartographic(wgs84);
```

#### 世界坐标数组转 84 坐标数组 transformCartesianArrayToWGS84Array

- @param

| 参数名       | type  | 描述         | 默认值 |
| ------------ | ----- | ------------ | ------ |
| cartesianArr | Array | 世界坐标数组 | -      |

- @returns

| 返回值   | type  | 描述        |
| -------- | ----- | ----------- |
| wgs84Arr | Array | 84 坐标数组 |

```js
let wgs84Arr = CM.Position.transformCartesianArrayToWGS84Array(cartesianArr);
```

#### 84 坐标数组转世界坐标数组 transformWGS84ArrayToCartesianArray

- @param

| 参数名   | type  | 描述        | 默认值 |
| -------- | ----- | ----------- | ------ |
| wgs84Arr | Array | 84 坐标数组 | -      |

- @returns

| 返回值       | type  | 描述         |
| ------------ | ----- | ------------ |
| cartesianArr | Array | 世界坐标数组 |

```js
let wgs84Arr = [
  { lng: 104.6926049397171, lat: 31.449924438393886, height: 0 },
  { lng: 104.70397349861078, lat: 31.444611031898347, height: 0 },
];
let cartesianArr = CM.Position.transformWGS84ArrayToCartesianArray(wgs84Arr);
```

#### 屏幕坐标转 84 坐标(纬度坐标) transformWindowToWGS84

- @param

| 参数名   | type   | 描述                    | 默认值 |
| -------- | ------ | ----------------------- | ------ |
| position | Object | 屏幕坐标，格式{x:1,y:1} | -      |

- @returns

| 返回值   | type   | 描述                       |
| -------- | ------ | -------------------------- |
| wgs84Obj | Object | 返回一个经纬度的 84 坐标。 |

```js
let wgs84 = CM.Position.transformWindowToWGS84(position);
```

#### 84 坐标(纬度坐标)转 屏幕坐标 transformWGS84ToWindow

- @param

| 参数名 | type   | 描述      |
| ------ | ------ | --------- |
| wgs84  | Object | 84 坐标。 |

- @returns

| 返回值   | type   | 描述                    | 默认值 |
| -------- | ------ | ----------------------- | ------ |
| position | Object | 屏幕坐标，格式{x:1,y:1} | -      |

```js
let wgs84 = { lng: 104.6926049397171, lat: 31.449924438393886, height: 0 };
let position = CM.Position.transformWGS84ToWindow(wgs84);
```
