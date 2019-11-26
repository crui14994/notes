## ES7 Async的使用

> Async函数已写入ES7标准中，通过async函数可以更友好直观的写异步代码。

在实际工作中，经常会遇到这样的场景：接口A需要的入参是接口B响应中的部分或全部内容，这时在执行请求接口A的代码时就需要等待接口B响应完成以后再执行，这就涉及异步调用。

#### 1. Promise例子

模拟异步请求：生成随机数，如果随机数小于1则认为是resolve的情况，执行resolve函数；如果大于1，则认为reject，执行reject函数。

```js
let p = new Promise(function (resolve, reject) {
  console.log('promise starting');
  let timeOut = Math.random() * 2;
  console.log('the random number is ' + timeOut + '...');

  // 模拟异步执行需要的时间
  setTimeout(function () {
    if (timeOut < 1) {
      console.log('返回结果如预期，调用resolve()...');
      resolve('200 OK');
    } else {
      console.log('没得到预期返回结果，调用reject()...');
      reject('请求超时：' + timeOut + 'second ...');
    }
  }, timeOut * 1000);
});

p.then(function (resolveValue) {
  console.log(resolveValue);
}).catch(function (rejectReason) {
  console.log(rejectReason);
});
```

模拟promise强大之处：链式调用

```js
let p = new Promise(function (resolve, reject) {
  console.log('直接返回resolve的promise');
  resolve(5);
});

let multiply = function (input) {
  return new Promise(function (resolve, reject) {
    console.log('计算' + input + '*' + input + '...');

    // 设置1s的计算延时，同样，认为为resolve的情况
    setTimeout(resolve, 1000, input * input);
  });
};

let add = function (input) {
  return new Promise(function (resolve, reject) {
    console.log('计算' + input + '+' + input + '...');
    setTimeout(resolve, 1000, input + input);   
  });
};

p.then(multiply)
 .then(add)
 .then(multiply)
 .then(add)
 .then(function (result) {
    console.log('最终结果是' + result);
 });
```

#### 2. Async函数

> 调用Async函数时会自动返回一个Promise对象：当这个异步函数返回预期值时，Promise会调用resolve方法处理这个预期值；如果这个异步函数抛出异常或者返回非法值时，Promise会调用reject方法进行处理。

#####  (1) .Async函数本身的语法为：

```js
async function name([param[, param[, ... param]]]) {
   statements
}
```

在普通函数前面加async关键字就变成了Async函数。

#####  (2) .await表达式

通常Async函数都会搭配await表达式和try-catch语句一起使用，代码格式为：

```js
async function myFirstAsyncFunction() {
  try {
    let fulfilledValue = await promise;
  }
  catch (rejectedValue) {
    // 捕获异常
  }
}
```

#####  (3) .注意事项

- await表达式必须放在Async函数中使用；

- await表达式后面可以跟一个Promise对象或者任何待解析的值（通常都是promise对象，不然没啥意义了），在等待Promise返回值时，Async函数暂停执行await表达式后面的代码，但不会阻塞JS主线程，即Async函数后面的代码正常执行。

#### 3. 重写promise的例子

模拟异步请求

```js
// 模拟异步请求生成的promise对象
let p = new Promise(function (resolve, reject) {
  console.log('promise starting');
  let timeOut = Math.random() * 2;
  console.log('the random number is ' + timeOut + '...');

  // 模拟异步执行需要的时间
  setTimeout(function () {
    if (timeOut < 1) {
      console.log('返回结果如预期，调用resolve()...');
      resolve('200 OK');
    } else {
      console.log('没得到预期返回结果，调用reject()...');
      reject('请求超时：' + timeOut + 'second ...');
    }
  }, timeOut * 1000);
});

(async function () {
  try {
    console.log(111);
    var resolvedP = await p; // promise返回结果之前，函数暂停执行
    console.log(222);
    console.log(resolvedP);
  } catch (error) {
    console.log(333);
    console.log(error);
  }
})();

console.log(444); // await等待promise的时候并不阻塞JS主线程，先于console.log(222)或者console.log(333)执行

```

promise链式写法重写

```js
let p = new Promise(function (resolve, reject) {
  console.log('直接返回resolve的promise');
  resolve(5);
});

let multiply = function (input) {
  return new Promise(function (resolve, reject) {
    console.log('计算' + input + '*' + input + '...');

    // 设置1s的计算延时，同样，认为为resolve的情况
    setTimeout(resolve, 1000, input * input);
  });
};

let add = function (input) {
  return new Promise(function (resolve, reject) {
    console.log('计算' + input + '+' + input + '...');
    setTimeout(resolve, 1000, input + input);   
  });
};

(async function () {
  let a = await p;
  let b = await multiply(a);
  let c = await add(b);
  let d = await multiply(c);
  let e = await add(d);
  console.log('最终结果是' + e)
})();
```

#### 参考文章

[Async函数和Promise对象](https://xiaogliu.github.io/2017/07/16/async-function-promise-object/)

[async 函数的含义和用法](http://www.ruanyifeng.com/blog/2015/05/async.html)
