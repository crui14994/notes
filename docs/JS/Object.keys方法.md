## Object.keys方法

#### 在实际开发中，我们有时需要知道对象的所有属性; 

ES5 引入了Object.keys方法，成员是参数对象自身的（不含继承的）所有可遍历（ enumerable ）属性的键名。

- 传入对象，返回属性名

    ```js
    var data={a:1,b:2,c:9,d:4,e:5};
        console.log(Object.keys(data));//["a", "b", "c", "d", "e"]
        Object.keys(data).map((key,item)=>{
            console.log(key,data[key]);//key=>属性名    data[key]=>属性值
    });
    ```

- 传入字符串，返回索引

    ```js
    var str = 'ab1234';
    console.log(Object.keys(obj));  //[0,1,2,3,4,5]
    ```

- 传入数组 返回索引

    ```js
    var arr = ["a", "b", "c"];
        console.log(Object.keys(arr)); // console: ["0", "1", "2"]
    ```

- 构造函数 返回空数组或者属性名

    ```js
    function Pasta(name, age, gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.toString = function () {
                return (this.name + ", " + this.age + ", " + this.gender);
        }
    }

    console.log(Object.keys(Pasta)); //console: []

    var spaghetti = new Pasta("Tom", 20, "male");
    console.log(Object.keys(spaghetti)); //console: ["name", "age", "gender", "toString"]

    ```

#### 扩展

1. Object.values()

Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（ enumerable ）属性的***键值***。

2. Object.entries()

Object.entries方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（ enumerable ）属性的***键值对数组***。