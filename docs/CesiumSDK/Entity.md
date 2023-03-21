# Entity

## 根据 id 获取一个实体 getEntityById

- @param

  id : 实体 id

- @returns

  entity ： entity 对象。如：

  ```js
  let entity = CM.Entity.getEntityById(id);
  ```

## 根据 id 删除一个实体 removeEntityById

- @param

  id : 实体 id

  ```js
  CM.Entity.removeEntityById(id);
  ```

## 删除所有实体 removeAllEntity

```js
CM.Entity.removeAllEntity(id);
```

## 注册 Entity 点击事件监听 onClick

- @param

  callback : 返回 entity 实体对象;如果当前点击只有一个实体返回当前实体，如果有多个实体返回所有实体对象数组.

  ```js
  CM.Entity.onClick((entity) => {});
  ```


## 注销点击事件 removeClick

  ```js
  CM.Entity.removeClick();
  ```


  ## 注册 Entity 拖拽事件 entityMove

  ```js
  CM.Entity.entityMove();
  ```


## 注销点击事件 removeEntityMove

  ```js
  CM.Entity.removeEntityMove();
  ```