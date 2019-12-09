### TypeScript笔记

#### 安装TypeScript包

```js
npm install typescript -g
```

#### 使用步骤

1. npm init -y来初始化项目，生成package.json文件。

2. 在终端中输入tsc --init；创建tsconfig.json文件，它是一个TypeScript项目的配置文件，可以通过读取它来设置TypeScript编译器的编译参数。

3. 安装@types/node,使用cnpm install @types/node --dev-save进行安装。这个主要是解决模块的声明文件问题。

4. 编写ts文件。

5. 在Vscode的任务菜单下，打开运行生成任务，然后选择tsc：构建-tsconfig.json，这时候就会生成一个helloWorld.js文件。

5. 在终端中输入node 文件名.js就可以看到结果了。

#### 变量类型

TypeScript最大的一个特点就是变量是强类型的，也就是说，在声明变量的时候，我们必须给他一个类型。比如：字符串、数字、布尔，枚举........ 

TypeScript中的数据类型有：

- Undefined :

- Number:数值类型;

- string : 字符串类型;

- Boolean: 布尔类型；

- enum：枚举类型；

- any : 任意类型，一个牛X的类型；

- void：空类型；

- Array : 数组类型;

- Tuple : 元祖类型；

- Null ：空类型。

>在TypeScrip中有几种特殊的Number类型 

- NaN：它是Not a Number 的简写，意思就是不是一个数值。如果一个计算结果或者函数的返回值本应该是数值，但是由于种种原因，他不是数字。出现这种状况不会报错，而是把它的结果看成了NaN。

- Infinity :正无穷大。

- -Infinity：负无穷大。

##### enum 类型

这个世界有很多值是多个并且是固定的，比如：

- 世界上人的类型：男人、女人、中性

- 一年的季节：春、夏、秋、冬 ，有四个结果。

    这种变量的结果是固定的几个数据时，就是我们使用枚举类型的最好时机：

    ```js
    enum REN{ nan , nv ,yao}
    console.log(REN.yao)  //返回了2，这是索引index，跟数组很想。
    ```
    如果我们想给这些枚举赋值，可以直接使用=来进行赋值。

    ```js
    enum REN{
        nan = '男',
        nv = '女',
        yao= '妖'
    }
    console.log(REN.yao)  //返回了妖 这个字
    ```

##### any类型

一个写惯了前端的人，有时候不自觉的就分不清类型了。这是个不好的习惯，也是前端的痛，就因为这个原因，JavaScript也多次被人诟病说大型项目不适合用JavaScript。但是习惯一旦养成，改是需要时间和磨练的。TypeScript友好的为我们提供了一种特殊的类型any，比如我们在程序中不断变化着类型，又不想让程序报错，这时候就可以使用any了。

#### TypeScript的函数

我们可以把功能相近的需求封装成一个独立的代码块，每次传入不同的变量或参数，就可以实现不同的结果。

```js
function search(age:number):string{
    return '找到了'+age+'岁的学生' 
}
var age:number = 18
var result:string = search(age)
console.log(result)
```

需要注意的是：

- 声明（定义）函数必须加 function 关键字；

- 函数名与变量名一样，命名规则按照标识符规则；

- 函数参数可有可无，多个参数之间用逗号隔开；

- 每个参数参数由名字与类型组成，之间用分号隔开；

- 函数的返回值可有可无，没有时，返回类型为 void；

- 大括号中是函数体。

TypeScript的函数参数是比较灵活的，它不像那些早起出现的传统语言那么死板。在TypeScript语言中，函数的形参分为：可选形参、默认形参、剩余参数形参等。

1. 有可选参数的函数

    可选参数，就是我们定义形参的时候，可以定义一个可传可不传的参数。这种参数，在定义函数的时候通过?标注。

2. 有默认参数的函数

    有默认参数就更好理解了，就是我们不传递的时候，他会给我们一个默认值;通过=标注。

3. 有剩余参数的函数

    有时候我们有这样的需求，我传递给函数的参数个数不确定。剩余参数就是形参是一个数组，传递几个实参过来都可以直接存在形参的数组中。

    ```js
    function search(...xuqiu:string[]):string{
    
        let  yy:string = '找到了'
        for (let i =0;i<xuqiu.length;i++){
            yy = yy + xuqiu[i]
            if(i<xuqiu.length){
                yy=yy+'、'
            }
        }
        yy=yy+'的学生'
        return yy

    }

    var result:string  =  search('22岁','长腿','瓜子脸');
    console.log(result)
    ```

#### 在TS中使用箭头函数

箭头函数是 ES6 中新增的函数定义的新方式，我们的 TypeScript 语言是完全支持 ES6 语法的。箭头函数定义的函数一般都用于回调函数中。

```js
var add = (n1:number,n2:number):number=>{
    return n1+n2
}

console.log(add(1,4))
```

#### 引用类型-数组

>TypeScript中的数据分为值类型和引用类型。

在TypeScript中也给我们提供了一些引用类型，例如：Array（数组）、String（字符串）、Date（日期对象）、RegExp（正则表达式）等。我们将用几节课的时间来学习这些用用类型，以及其中封装的常用方法和属性。

##### 字面量赋值法：直接使用“[ ]”对数组进行赋值。

```js
//定义一个空数组，数组容量为0
let arr1:number[] = [] 
//定义一个数组时，直接给数组赋值
let arr2:number[] = [1,2,3,4,5]
//定义数组 的同事给数组赋值
let arr3:Array<string> = ['产品','技术','运营']
let arr4:Array<boolean> = [ true,false,false]
```

##### 构造函数赋值法

```js
let arr1:number[] = new Array()
let ara2:number[] = new Array(1,2,3,4,5)
let arr3:Array<string> = new Array('产品','技术','运营')
let arr4:Array<boolean> = new Array(true,false,false)
```
##### 元祖，一种特殊的数组

元祖是一种特殊的数组，元祖类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。比如，你可以定义一对值分别为string和number类型的元祖。元祖在实际开发中使用的非常少.

```js
//声明一个元祖类型
let x : [string,number]
//正确的初始化
x = ['hello',10]
//错误的初始化方法
x = [10,'hello']
```

#### 引用类型-字符串啊

字符串的两种类型

- 基本类型字符串：由单引号或者双引号括起来的一串字符串。

- 引用类型字符串：用new 实例化的 String类型。

JavaScript的开发人员为了大家更容易的操作字符串，有了引用类型的字符串就可以给字符串增加一系列方法了。

```js
let jspang:string = '产品'
let jspanga:String = new String("chanping")
console.log(jspang) //技术胖
console.log(jspanga) // [String: 'chanping']
```

>这两种声明字符串的方法没有什么不同。基本类型的字符串可以直接使用引用类型的属性和方法。

#### 引用类型-日期对象

日期对象是Date的实例，可以使用构造函数的方法进行创建。并且构造函数中可以传递多种类型的参数。

1. 不传递任何参数

    ```js
    let d:Date = new Date()
    console.log(d) //2018-09-06T06:48:12.504Z
    ```
    
2. 传递一个整数，这个整数代表的是距离1970-01-01 00:00:00的毫秒数

    ```js
    let d:Date = new Date(1000)
    let da:Date = new Date(2000)
    console.log(d)  //1970-01-01T00:00:01.000Z
    console.log(da) //1970-01-01T00:00:02.000Z
    ```
    
3. 传递一个字符串

    字符串的格式常用:yyyy/MM/dd hh:mm:ss，yyyy-MM-dd hh:mm:ss，yyyy-MM-ddThh:mm:ss等,具体可以参看下面的例子。

    ```js
   let d1:Date = new Date('2018/09/06 05:30:00')
    let d2:Date = new Date('2018-09-06 05:30:00')
    let d3:Date = new Date('2018-09-06T05:30:00')
    console.log(d1)
    console.log(d2)
    console.log(d3)
    ```

    
4. 传递表示年月日时分秒的变量

    ```js
   let d:Date = new Date(year,month,day,hours,minutes,seconds,ms);
    ```

#### 引用类型-正则表达式

>RegExp对象包含两个方法：test( )和exec( ),功能基本相似，用于测试字符串匹配。

test(string) ：在字符串中查找是否存在指定的正则表达式并返回布尔值，如果存在则返回 true，不存在则返回 false。

```js
let reg1:RegExp =  /jspang/i
let website:string = 'jspang.com'
let result:boolean = reg1.test(website)
console.log(result)    //true
```

exec(string) : 用于在字符串中查找指定正则表达式，如果 exec() 方法执行成功，则返回包含该查找字符串的相关信息数组。如果执行失败，则返回 null。

```js
let reg1:RegExp =  /jspang/i
let website:string = 'jspang.com'
console.log(reg1.exec(website))
//[ 'jspang', index: 0, input: 'jspang.com' ]
```

####  面向对象编程-类的声明和使用

类的定义:先用class关键字声明了一个类，并在里边声明了name和age属性。constructor为构造函数。构造函数的主要作用是给类中封装的属性进行赋值。

```js
class XiaoJieJie{
    name:string;
    age:number;
    constructor(name:string,age:number){
        this.name = name
        this.age = age 
    }
    say(){
        console.log('小哥哥好')
    }
}

let jiejie:XiaoJieJie = new XiaoJieJie('范冰冰',18)

console.log(jiejie)
jiejie.say()
```

#### 面向对象编程-修饰符

TypeScript语言和Java还有C#很像（因为我只会这两个面向对象的语言），类中属性的访问可以用访问修饰符来进行限制。访问修饰符分为：public、protected、private。

- public:公有修饰符，可以在类内或者类外使用public修饰的属性或者行为，默认修饰符。

- protected:受保护的修饰符，可以本类和子类中使用protected修饰的属性和行为。

- private : 私有修饰符，只可以在类内使用private修饰的属性和行为

```js
class XiaoJieJie2{
    public sex:string
    protected name:string
    private age:number
    public constructor(sex:string,name:string,age:number){
        this.sex=sex
        this.name=name
        this.age=age
    }
    public sayHello(){
        console.log('小哥哥好')
    }

    protected sayLove(){
        console.log('我爱你')
    }
}

var jiejie2:XiaoJieJie2 = new XiaoJieJie2('女','小丽',22)

console.log(jiejie2.sex)
console.log(jiejie2.name)   //报错
console.log(jiejie2.age)    //报错
jiejie2.sayHello()
jiejie2.sayLove()    //报错

```

##### 只读属性修饰符

使用readonly修饰符将属性设置为只读，只读属性必须在生命时或者构造函数里被初始化（注意）。

```js
class Man{
    public readonly sex:string = '男'
}

var man:Man = new Man()
man.sex='女'  //报错
```

#### 面向对象编程-继承和重写

##### 类的继承

继承：允许我们创建一个类（子类），从已有的类（父类）上继承所有的属性和方法，子类可以新建父类中没有的属性和方法。

```js
class Jspang{
    public name:string
    public age : number
    public skill: string
    constructor(name:string,age:number,skill:string){
        this.name = name
        this.age = age
        this.skill = skill
    }
    public interest(){
        console.log('找小姐姐')
    }
}

let jspangObj:Jspang = new Jspang('技术胖',18,'web')
jspangObj.interest()
```

程序实现:

```js
class JsShuai extends Jspang{
    public xingxiang:string = '帅气'
    public zhuangQian(){
        console.log('一天赚了一个亿')
    }
}

let shuai = new JsShuai("技术帅",5,'演讲')
shuai.interest()
shuai.zhuangQian()
```

>但是有一点需要我们注意，TypeScript不支持多重继承。

##### 类方法的重写

重写就是在子类中重写父类的方法。例如，我的儿子“技术帅”发现兴趣爱好是找小姐姐，完成不了“”一天赚一个亿“”的目标，它需要多个兴趣，开平台网站。这时候我们就用到了重写。看下面的列子代码：

```js
class JsShuai extends Jspang{
    public xingxiang:string = '帅气'
    public interest(){
        super.interest()
        console.log('建立电商平台')
    }
    public zhuangQian(){
        console.log('一天赚了一个亿')
    }
}

```

先是继承了父类的方法，然后通过super关键字调用了父类的方法，实现了技能的增加。

#### 面向对象编程-接口

前端也有接口的定义，特别如果你要靠着前端技术作一个全栈，那接口的编写也是必不可少的一项技能。

>在面向对象的语言中，术语interface经常被用来定义一个不包含数据和逻辑代码但是用来签名定义了行为的抽象类型。

##### 定义接口的关键字是interface。我们现在就来定义一个接口:

```js
interface Husband {
    sex:string
    interest:string
}
let myhusband:Husband ={ sex:'男',interest:'看书、做作业'}
console.log(myhusband)

//我们通过接口，定义了一个学生的接口，并且给他了两个必选项：性别和兴趣爱好
```

##### 可选参数的接口

如果我们有一些可选项，这些并不是都需要显示出来的，在有些情况下，我们只需要传入部分参数。我们可以使用问好的形式来设置可选参数。

```js
interface Husband {
    sex:string
    interest:string
    answer?:Boolean
}
let myhusband:Husband ={ sex:'男',interest:'看书、做作业',answer:true}
console.log(myhusband)

```

##### 规范函数类型接口

我们还可以使用接口来规范函数类型的接口，比如现在要找老公这件事，我们规定有一些资源，然后我们需要哪些资源，在函数中进行匹配，最后返回是否匹配成功。

```js
interface  SearchMan{
    (source:string,subString:string):boolean
}

let mySearch:SearchMan

mySearch = function(source:string,subString:string):boolean{
    let flag =source.search(subString)
    return (flag != -1)
} 

console.log(mySearch('高、富、帅、德','胖')) //false
```

#### 面向对象编程-命名空间

在制作大型应用的时候，为了让程序更加有层次感和变量之间不互相干扰，我们可以使用命名空间来构建程序。举个小例子：比如“德华”这件事，帅哥也有叫德华的，二师兄也有叫德华的;那我们要如何区分.

```js
namespace shuaiGe{
    export class Dehua{
        public name:string = '刘德华'
        talk(){
            console.log('我是帅哥刘德华')
        }
    }
}

namespace bajie{
    export class Dehua{
        public name:string = '马德华'
        talk(){
            console.log('我是二师兄马德华')
        }
    }
}

let dehua1:shuaiGe.Dehua   = new shuaiGe.Dehua()
let dehua2:shuaiGe.Dehua   = new bajie.Dehua()
dehua1.talk()
```