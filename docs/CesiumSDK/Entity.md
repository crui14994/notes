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

| 参数名   | type     | 描述                                                                                                     | 默认值 |
| -------- | -------- | -------------------------------------------------------------------------------------------------------- | ------ |
| callback | Function | 回调函数；返回 entity 实体对象;如果当前点击只有一个实体返回当前实体，如果有多个实体返回所有实体对象数组。 | -      |

```js
CM.Entity.onClick((entity) => {});
```

#### 注销点击事件 removeClick

```js
CM.Entity.removeClick();
```

#### 注册 Entity 拖拽事件 entityMove

```js
CM.Entity.entityMove();
```

#### 注销拖拽事件 removeEntityMove

```js
CM.Entity.removeEntityMove();
```
