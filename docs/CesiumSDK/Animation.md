# Animation

## 设置视图到某一点 setView

- @param

| 参数名   | type   | 描述    | 默认值 |
| -------- | ------ | ------- | ------ |
| position | Object | 84 坐标 | -      |

```js
let point = CM.Animation.setView(114.40782845, 30.51011682, 5000.0);
```

## 开始自转 startIcrf

```js
CM.Animation.startIcrf();
```

## 停止自转 stopTcrf

```js
CM.Animation.stopTcrf();
```

## 定位到某个目标 viewerFlyTo

如果在场景中已经添加了各个要素，需要定位到某个目标，显然 viewer. fyTo()是比较合适的；也就是说目标是要素，viewer. fyTo()比较合适。

把相机飞到 entity, entities, 或者 data source 位置。在这些数据还加载和渲染完成后，才能触发 fyTo。

- @param

| 参数名   | type     | 描述                                            | 默认值 |
| -------- | -------- | ----------------------------------------------- | ------ |
| target   | Object   | 可以是 entity、entities、tilse 或者 data source | -      |
| callback | Function | 定位完成的回调函数                              | -      |
| duration | Function | 飞行时间                                        | 3      |

```js
let point = CM.Animation.viewerFlyTo(target, () => {}, 3);
```

## 定位到某个坐标 cameraFlyTo

如果是设置相机位置，Camera.fyTo()比较合适。

- @param

| 参数名   | type     | 描述               | 默认值 |
| -------- | -------- | ------------------ | ------ |
| position | Object   | 坐标               | -      |
| callback | Function | 定位完成的回调函数 | -      |
| duration | Function | 飞行时间           | 3      |

```js
let point = CM.Animation.cameraFlyTo(position, () => {}, 3);
```
