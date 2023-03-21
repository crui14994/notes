# Position

## 获取相机位置及姿态 getCameraAttitude

- @returns

  返回相机位置及姿态。如：

  ```js
  let res = CM.Position.getCameraAttitude();
  ```

## 根据屏幕坐标 获取世界坐标、地形坐标、场景坐标 getClickPosition

- @param

  eventPosition :event.position

  type :1-世界坐标（地图/椭球体表面的坐标） 2-地形坐标 3-场景坐标 ；默认为1

- @returns

  返回指定类型的坐标。如：

  ```js
  //当前点击视线与椭球面相交处的坐标
  let position1 = CM.Position.getClickPosition(1);

  //只能求交于地形，不包括模型、倾斜摄影表面，能获取加载地形后的坐标，pick(ray, scene, result) → Cartesian3|undefined
  let position2 = CM.Position.getClickPosition(2);

  //根据窗口坐标，从场景的深度缓冲区中拾取相应的位置，返回笛卡尔坐标，不仅可以求交地形，还可以求交除地形以外其他所有写深度的物体。pickPosition(windowPosition, result) → Cartesian3
  let position3 = CM.Position.getClickPosition(3);
  ```

## 根据经纬度获取terrain高程，精度为m getHeigthByLonLat

- @param

  lng :经度

  lat :纬度

- @returns

  返回一个Promise对象。如：

  ```js
  CM.Position.getHeigthByLonLat('35.125','104.5').then(height=>{
      console.log(height)
  });
  ```

## 世界坐标转换为 84 坐标(纬度坐标) transformCartesianToWGS84

- @param

  cartesian：世界坐标

- @returns

  返回一个经纬度高度的84 坐标。如：

  ```js
  let wgs84 = CM.Position.transformCartesianToWGS84(cartesian);
  ```
	
## 84坐标(纬度坐标)转换为世界坐标 transformWGS84ToCartesian

- @param

  position : 经纬度高度的84 坐标

- @returns

  Cartesian3 :世界坐标。如：

  ```js
  let wgs84 = CM.Position.transformWGS84ToCartesian(position);
  ```

## 84纬度坐标转换为 84弧度坐标 transformWGS84ToCartographic

- @param

  position : 经纬度高度的84 坐标

- @returns

  cartographic :84弧度坐标。如：

  ```js
  let cartographic = CM.Position.transformWGS84ToCartographic(position);
  ```

	
## 世界坐标数组转 84 坐标数组 transformCartesianArrayToWGS84Array

- @param

  cartesianArr : 世界坐标数组

- @returns

  wgs84Arr :84坐标数组。如：

  ```js
  let wgs84Arr = CM.Position.transformCartesianArrayToWGS84Array(cartesianArr);
  ```

	
## 84 坐标数组转世界坐标数组 transformWGS84ArrayToCartesianArray

- @param

  wgs84Arr :84坐标数组。

- @returns

  cartesianArr : 世界坐标数组。如：

  ```js
  let wgs84Arr = CM.Position.transformWGS84ArrayToCartesianArray(cartesianArr);
  ```

		
## 屏幕坐标转84坐标(纬度坐标) transformWindowToWGS84

- @param

  position : 屏幕坐标，格式{x:1,y:1}

- @returns

  wgs84 :84坐标。如：

  ```js
  let wgs84 = CM.Position.transformWindowToWGS84(position);
  ```

			
## 84坐标(纬度坐标)转 屏幕坐标 transformWGS84ToWindow

- @param

  wgs84 :84坐标。如：

- @returns

	position : 屏幕坐标，格式{x:1,y:1}

  ```js
  let position = CM.Position.transformWGS84ToWindow(wgs84);
  ```