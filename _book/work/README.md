## 知识点收集

---

### 注意事项

#### - 箭头函数

箭头函数没有大括号会默认return；

如果有大括号则需要自己return，否则不会返回任何对象。

#### - forEach

forEach中使用 return 没有办法中止或者跳出 forEach() 循环，除了抛出一个异常。如：

```js
unction foreachArr(arr,id){
    arr.forEach(item=>{
        console.log('id:'+item.id);
        if(item.id==id){
            return;
        }
    })
}

let person=[{id:1,name:'Nancy',age:24},{id:2,name:'Carol',age:26},{id:3,name:'Lucy',age:20}];
foreachArr(person,2);
//打印出来的结果：
//[Log] id:1
//[Log] id:2
//[Log] id:3  怎么还有 id:3? 
```

和for循环的对比

```js
function forinArr(arr,id){
    for(let i in arr){
        console.log('id:'+arr[i].id);
        if(arr[i].id==id){
            return;
        }
    }
}
forinArr(person,2);
//打印出来的结果：
[Log] id:1
[Log] id:2
```

[使用forEach、some、every、find、findIndex的正确姿势](https://www.jianshu.com/p/91d740ad0ab9)

