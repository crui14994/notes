## Entity

#### 根据 id 获取一个实体 getEntityById

- @param

| 参数名 | type   | 描述    | 默认值 |
| ------ | ------ | ------- | ------ |
| id     | String | 实体 id | -      |

- @returns

| 返回值    | type   | 描述          | 默认值 |
| --------- | ------ | ------------- | ------ |
| entityObj | Object | entity 对象。 | -      |

```js
let entity = CM.Entity.getEntityById(id);
```

#### 根据 id 删除一个实体 removeEntityById

- @param

| 参数名 | type   | 描述    | 默认值 |
| ------ | ------ | ------- | ------ |
| id     | String | 实体 id | -      |

```js
CM.Entity.removeEntityById(id);
```

#### 删除所有实体 removeAllEntity

```js
CM.Entity.removeAllEntity(id);
```

#### 注册 Entity 点击事件监听 onClick

- @param

| 参数名   | type     | 描述                                                                                                      | 默认值 |
| -------- | -------- | --------------------------------------------------------------------------------------------------------- | ------ |
| callback | Function | 回调函数；返回 entity 实体对象;如果当前点击只有一个实体返回当前实体，如果有多个实体返回所有实体对象数组。 | -      |

```js
CM.Entity.onClick((entity) => {});
```

#### 注销点击事件 removeClick

```js
CM.Entity.removeClick();
```

#### 注册 Entity 拖拽事件 entityMove

- @param

| 参数名   | type     | 描述                                   | 默认值 |
| -------- | -------- | -------------------------------------- | ------ |
| callback | Function | 回调函数；返回当前托动 entity 实体对象 | -      |

```js
CM.Entity.entityMove((entity) => {});
```

#### 注销拖拽事件 removeEntityMove

```js
CM.Entity.removeEntityMove();
```

#### 加载聚合图标点 loadClusterMarker

- @param

| 参数名   | type   | 描述                                         | 默认值      |
| -------- | ------ | -------------------------------------------- | ----------- |
| position | Object | 84 坐标                                      | -           |
| myData   | Object | 自定义的数据，在监听点击事件时根据此属性获取 | -           |
| imgUrl   | Object | 图标文件，通过 require 获取                  | -           |
| imgSize  | Object | 图标大小                                     | {w:40,h:40} |

- @returns

| 返回值        | type   | 描述             |
| ------------- | ------ | ---------------- |
| clusterMarker | Object | 返回聚合图标点。 |

```js
let clusterMarker = CM.Entity.loadClusterMarker(position, myData, imgUrl);
```

#### 加载自定义的聚合图标点 loadCustomClusterMarker

- @param

| 参数名    | type   | 描述                       | 默认值 |
| --------- | ------ | -------------------------- | ------ |
| entityObj | Object | 参考 cesium 的 entity 配置 | -      |

- @returns

| 返回值        | type   | 描述             |
| ------------- | ------ | ---------------- |
| clusterMarker | Object | 返回聚合图标点。 |

```js
let clusterMarker = CM.Entity.loadCustomClusterMarker(entityObj);
```

#### 将所有普通图标点转换为聚合图标点 pointToClusterMarker

- @returns

| 返回值            | type   | 描述                             | 默认值 |
| ----------------- | ------ | -------------------------------- | ------ |
| clusterDataSource | Object | 自定义的聚合图标 DataSource 对象 | -      |

```js
let clusterDataSource = CM.Entity.pointToClusterMarker();
```

#### 获取所有聚合图标自定义的 DataSource 对象 getClusterDataSource

- @returns

| 返回值            | type   | 描述                             | 默认值 |
| ----------------- | ------ | -------------------------------- | ------ |
| clusterDataSource | Object | 自定义的聚合图标 DataSource 对象 | -      |

```js
let clusterDataSource = CM.Entity.getClusterDataSource();
```

#### 开启聚合图标显示 openCluster

- @param

| 参数名            | type   | 描述                              | 默认值 |
| ----------------- | ------ | --------------------------------- | ------ |
| option            | Object | 参考 cesium 的 EntityCluster 配置 | -      |
| clusterIconConfig | Object | 聚合图标配置                      | -      |

- @returns

| 返回值            | type   | 描述                             |
| clusterDataSource | Object | 自定义的聚合图标 DataSource 对象 | -   |

###### clusterIconConfig

| 参数名    | type    | 描述                                             | 默认值 |
| --------- | ------- | ------------------------------------------------ | ------ |
| max       | Number  | 当聚合数量超过此值执行的配置;值为 0 时为默认配置 | -      |
| color     | String  | 聚合图标颜色                                     | -      |
| width     | Number  | 图标宽度                                         | -      |
| height    | Number  | 图标高度                                         | -      |
| fontColor | String  | 聚合图标字体图标                                 | -      |
| isImg     | Boolean | 是否使用自定义图片代替聚合图标                   | -      |
| imgUrl    | String  | 自定义图片                                       | -      |

```js
// clusterIconConfig默认配置
// let clusterIconConfig = [
//   {
//     max: 20, //当聚合数量超过此值执行的配置;值为0时为默认配置
//     color: "#0000ff", //聚合图标颜色
//     // isImg: true, //是否使用自定义图片代替聚合图标
//     // imgUrl: require('@/assets/logo.png'),
//     width: 72, //图标宽度
//     height: 72, //图标高度
//     fontColor: "#fff", //聚合图标字体图标
//   },
//   {
//     max: 12,
//     color: "#F8C71F",
//     // isImg: true,
//     // imgUrl: require('@/assets/logo.png'),
//     width: 56,
//     height: 56,
//     fontColor: "#fff",
//   },
//   {
//     max: 0,
//     color: "#FF1E1E",
//     // isImg: true,
//     // imgUrl: require('@/assets/logo.png'),
//     width: 56,
//     height: 56,
//     fontColor: "#fff",
//   },
// ];
let clusterDataSource = CM.Entity.openCluster(option, clusterIconConfig);
```

#### 关闭聚合图标显示 removeCluster

```js
CM.Entity.removeCluster();
```
