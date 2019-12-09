## 前端模块化（CommonJs,ES6 Module, AMD和CMD）

> 主要针对CommonJs和ES6 Module进行学习

#### commonJS

- 一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为global对象的属性。

- 输出模块变量的最好方法是使用module.exports对象。

- 加载模块使用require方法，该方法读取一个文件并执行，返回文件内部的module.exports对象

> commonJS用同步的方式加载模块。在服务端，模块文件都存在本地磁盘，读取非常快，所以这样做不会有问题。但是在浏览器端，限于网络原因，更合理的方案是使用异步加载，所以在浏览器端一般就不使用commonJS了

CommonJS规范规定，每个模块内部，module变量代表当前模块。这个变量是一个对象，它的exports属性（即module.exports）是对外的接口。加载某个模块，其实是加载该模块的module.exports属性。

```js
var x = 5;
var addX = function (value) {
  return value + x;
};

//一个一个 导出
module.exports.x = x;
module.exports.addX = addX;

//整体导出
module.exports = { x: x, addX:addX }
```

上面代码通过module.exports输出变量x和函数addX。

require方法用于加载模块。

```js
var example = require('./example.js');
console.log(example.x); // 5
console.log(example.addX(1)); // 6
```

> 为了方便，Node为每个模块提供一个exports变量，指向module.exports。这等同在每个模块头部，有一行这样的命令。

```js
var exports = module.exports;
```

造成的结果是，在对外输出模块接口时，可以向exports对象添加方法。

```js
exports.area = function (r) {
  return Math.PI * r * r;
};

exports.circumference = function (r) {
  return 2 * Math.PI * r;
};
```

#### ES6 Module

ES6 Module主要由两个命令构成：export和import。

- export命令：用于规定模块的对外接口

- import命令：用于输入其他模块提供的功能。

##### export命令

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量

```js
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export { firstName, lastName, year };
```

export命令除了输出变量，还可以输出函数或类（class）:

```js
export function multiply(x, y) {
  return x * y;
};
```

> 需要特别注意的是，export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。

```js
// 报错
export 1;

// 报错
var m = 1;
export m;
```

正确的写法为：

```js
// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};

// function和class的输出，也必须遵守这样的写法

// 报错
function f() {}
export f;

// 正确
export function f() {};

// 正确
function f() {}
export {f};
```

##### import 命令

使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。

```js
// main.js
import { firstName, lastName, year } from './profile.js';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

> 如果想为输入的变量重新取一个名字，import命令要使用as关键字，将输入的变量重命名。

```js
import { lastName as surname } from './profile.js';
```

##### export default 命令

从前面的例子可以看出，使用import命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。但是，用户肯定希望快速上手，未必愿意阅读文档，去了解模块有哪些属性和方法。

为了给用户提供方便，让他们不用阅读文档就能加载模块，就要用到export default命令，为模块指定默认输出。

```js
// export-default.js
export default function () {
  console.log('foo');
}
```

上面代码是一个模块文件export-default.js，它的默认输出是一个函数。

其他模块加载该模块时，import命令可以为该匿名函数指定任意名字。

```js
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```

>上面代码的import命令，可以用任意名称指向export-default.js输出的方法，这时就不需要知道原模块输出的函数名。需要注意的是，这时import命令后面，不使用大括号。

export default命令用在非匿名函数前，也是可以的

```js
// export-default.js
export default function foo() {
  console.log('foo');
}

// 或者写成

function foo() {
  console.log('foo');
}

export default foo;
```

上面代码中，foo函数的函数名foo，在模块外部是无效的。加载的时候，视同匿名函数加载。



参考：[Module的语法](http://es6.ruanyifeng.com/#docs/module#import-命令)

#### CommonJs和 ES6 Module 的区别

1. CommonJs导出的是变量的一份拷贝，ES6 Module导出的是变量的绑定（export default 是特殊的）  

2. CommonJs是单个值导出，ES6 Module可以导出多个

3. CommonJs是动态语法可以写在判断里，ES6 Module静态语法只能写在顶层

4. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。

```js
// CommonJS模块
let { stat, exists, readFile } = require('fs');

// 等同于
let _fs = require('fs');
let stat = _fs.stat;
let exists = _fs.exists;
let readfile = _fs.readfile;
```

> 上面代码的实质是整体加载fs模块（即加载fs的所有方法），生成一个对象（_fs），然后再从这个对象上面读取 3 个方法。这种加载称为“运行时加载”，因为只有运行时才能得到这个对象，导致完全没办法在编译时做“静态优化”。

ES6 模块不是对象，而是通过export命令显式指定输出的代码，再通过import命令输入。

```js
// ES6模块
import { stat, exists, readFile } from 'fs';
```

> 上面代码的实质是从fs模块加载 3 个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载，效率要比 CommonJS 模块的加载方式高。当然，这也导致了没法引用 ES6 模块本身，因为它不是对象。

#### AMD与CMD的比较

1. AMD：依赖前置，预执行（异步加载：依赖先执行）;偏浏览器端。

2. CMD：依赖就近，懒（延迟）执行（运行到需加载，根据顺序执行）；偏l浏览器端。

3. AMD用户体验好，因为没有延迟，依赖模块提前执行了; CMD性能好，因为只有用户需要的时候才执行

>- CommonJs用在服务器端，AMD和CMD用在浏览器环境

>- AMD 是 RequireJS 在推广过程中对模块定义的规范化产出。

>- CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。

>- AMD:提前执行（异步加载：依赖先执行）+延迟执行

>- CMD:延迟执行（运行到需加载，根据顺序执行）

