## es6 class及super关键字

#### 传统方法

JavaScript 语言中，生成实例对象的传统方法是通过构造函数。

```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

基本上，ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```


#### 取值函数（getter）和存值函数（setter）

与 ES5 一样，在“类”的内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

```js
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

> 上面代码中，prop属性有对应的存值函数和取值函数，因此赋值和读取行为都被自定义了。


#### 属性表达式

```js
let methodName = 'getArea';

class Square {
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```

> 上面代码中，Square类的方法名getArea，是从表达式得到的。


#### 静态方法

如果在一个方法前，加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

```js
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```

> 注意，如果静态方法包含this关键字，这个this指的是类，而不是实例。

```js
class Foo {
  static bar() {
    this.baz();
  }
  static baz() {
    console.log('hello');
  }
  baz() {
    console.log('world');
  }
}

Foo.bar() // hello
```

#### Class的继承

Class 可以通过extends关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

```js
class Point {
}

class ColorPoint extends Point {
}
```

#### super关键字

super这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

- 作为函数时，super()只能用在子类的构造函数之中，用在其他地方就会报错。

    > 子类必须在constructor方法中调用super方法，否则新建实例时会报错。如果不调用super方法，子类就得不到this对象.

    ```js
    class A {}

    class B extends A {
    constructor() {
        super();
    }
    }
    ```

    注意，super虽然代表了父类A的构造函数，但是返回的是子类B的实例，即super内部的this指的是B的实例;

    ```js
    class A {
    constructor() {
        console.log(new.target.name);
    }
    }
    class B extends A {
    constructor() {
        super();
    }
    }
    new A() // A
    new B() // B

    //上面代码中，new.target指向当前正在执行的函数。
    ```

    另一个需要注意的地方是，在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错。这是因为子类实例的构建，基于父类实例，只有super方法才能调用父类实例。

    ```js
    class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    }

    class ColorPoint extends Point {
    constructor(x, y, color) {
        this.color = color; // ReferenceError
        super(x, y);
        this.color = color; // 正确
    }
    }
    ```

- super作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。

    ```js
    class A {
    p() {
        return 2;
    }
    }

    class B extends A {
    constructor() {
        super();
        console.log(super.p()); // 2
    }
    }

    let b = new B();
    ```

    ```js
    class Parent{
        static myMethod(msg){
            console.log("static",msg);
        }
        myMethod(msg){
            console.log("instance",msg);
        }
    }

    class Child extends Parent{
        static myMethod(msg){
            super.myMethod(msg);
        }
        myMethod(msg){
            super.myMethod(msg);
        }
    }

    Child.myMethod("1"); //static 1

    let child = new Child();
    child.myMethod("2"); //instance 2
    ```

#### 参考：
[class继承](http://es6.ruanyifeng.com/#docs/class-extends)