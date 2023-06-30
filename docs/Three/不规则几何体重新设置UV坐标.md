## 不规则的 shape 形状重新设置 UV 坐标（r151.1 版本）

当使用 ShapeGeometry 创建不规则的图形时,geometry.attributes.uv 里面的 UV 坐标实际上是不对的；

UV贴图相关知识查看其它文档！

![geometry](/img/1.jpg)

#### 出现情况

如果直接进行贴图无法得到理想的贴图效果；


```js
...
const shape = new THREE.Shape();
...
const extrudeSettings = {
  depth: 1,
  bevelEnabled: true,
  bevelSegments: 1,
  bevelThickness: 0.2,
};
const geometry = new THREE.ExtrudeGeometry(shape, extrudeSettings);
console.log(geometry)

//重新定义uv坐标
// setGeometryUV(geometry)

const texture = new THREE.TextureLoader().load('/data/img/china.png');
texture.wrapS = THREE.RepeatWrapping;
texture.wrapT = THREE.RepeatWrapping;
texture.repeat.set(1, 1);
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);
```

![geometry](/img/2.jpg)


#### 解决方法

此时我们需要对此 geometry 的 UV 坐标重新定义！封装 setGeometryUV 方法：

```js
//geometry 为three创建的不规则几何对象
function setGeometryUV(geometry) {
  if (!geometry.boundingBox) {
    geometry.computeBoundingBox();
  }
  let arr = [];
  let offset = [0 - geometry.boundingBox.min.x, 0 - geometry.boundingBox.min.y];
  let range = [
    geometry.boundingBox.max.x - geometry.boundingBox.min.x,
    geometry.boundingBox.max.y - geometry.boundingBox.min.y,
  ];
  geometry.attributes.position.array.forEach((item, index) => {
    if ((index + 1) % 3 == 1) {
      arr.push((item + offset[0]) / range[0]);
    } else if ((index + 1) % 3 == 2) {
      arr.push((item + offset[1]) / range[1]);
    }
  });
  let uvs = new Float32Array(arr);
  geometry.attributes.uv = new THREE.BufferAttribute(uvs, 2);
}
```

在创建 geometry 后执行 setGeometryUV 方法，得到正确的贴图：

![geometry](/img/3.jpg)
