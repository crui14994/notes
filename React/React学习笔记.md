#### 脚手架的安装

```javascript
//安装脚手架工具

npm install -g create-react-app

//创建项目

create-react-app demo01
```



#### JSX简介

JSX就是Javascript和XML结合的一种格式。React发明了JSX，可以方便的利用HTML语法来创建虚拟DOM，当遇到<，JSX就当作HTML解析，遇到{就当JavaScript解析.

#### Fragment标签讲解

在写一个组件的时候，组件的最外层都需要有一个包裹。

但是布局就偏不需要这个最外层的标签怎么办?比如我们在作Flex布局的时候,外层还真的不能有包裹元素；此时就可以使用<Fragment>标签。

```javascript
import React,{Component,Fragment } from 'react'

//等同于
import React from 'react';
const  Component = React.Component;
const  Fragment = React.Fragment;

```
将最外层div替换为Fragment就行了


```javascript
class App extends Component {
    render() {
        return (
            <Fragment>
                <ul className="my-list">
                    <li>{false ? 'XXXXX' : '******'}</li>
                    <li>I love React</li>
                </ul>
            </Fragment>
        )
    }
}
```



#### 绑定事件(如果事件中需要使用到this)需要注意的事项

> 错误示例(会提示错误，因为this指向不对)：

```html
<input  onChange={this.inputChange} />
```

> 解决方法：

1. 使用箭头函数（推荐）

   ```js
   <input onChange={ (e)=> this.inputChange(e) } />
   ```

2. 重新用bind设置一下指向(ES6的语法)

   ```html
   <input onChange={this.inputChange.bind(this)} />
   ```



#### React中改变值需要使用this.setState方法(当this.setState()被调用的时候，React会重新调用render方法来重新渲染UI)

>State 的更新是异步的;调用setState，组件的state并不会立即改变，setState只是把要修改的状态放入一个队列中，React会优化真正的执行时机，并且React会出于性能原因，可能会将多次setState的状态修改合并成一次状态修改。所以不要依赖当前的State，计算下个State。

this.setState中对数组进行操作必须使用返回新数组的方法；如：concat方法。

```js
this.setState({
    list: this.state.list.concat(service);
    // list: this.state.list.push(service); 报错
})
```

push()是在原数组的基础上修改的，执行push()方法后原数组的值也会变；

concat()是先把原数组复制到一个新的数组，然后在新数组上进行操作，所以不会改变原数组的值。

#### constructor()、super()、super(props)

1. 只要存在constructor就要调用super()；很多时候需要在constructor中访问this,当没有调用super()时，this还没有被初始化，所以不能使用this.

2. 什么时候必须要调用super(props)呢？当需要在constructor中访问**this.props**的情况下.

3. 即使没有constructor，依然可以在render中使用this.props，这是因为react在初始化class后，会将props自动设置到this中，所以在任何地方都可以直接访问this.props，除了一个地方：**constructor**


#### React是禁止直接操作state的

比如要删除一个数据：

```js
deleteService(index) {
    //正确的做法
    const {list} = this.state;
    list.splice(index, 1);
    this.setState({
        list: list
    })

    //错误的做法
    // this.state.list.splice(index, 1)
    // this.setState({
    //     list: this.state.list
    // })
}
```

虽然上面错误的方法也管用,但是在后期的性能优化上会有很多麻烦,所以一定不要这样操作.

#### JSX防踩坑的几个地方

1. JSX中的class陷阱

    要把class换成className，它是防止和js中的class类名 冲突，所以要求换掉。

2. JSX中<label>标签的坑

    label是html中的一个辅助标签，在文本框前面加入一个<label>；浏览效果虽然可以正常，但console里还是有红色警告提示的。大概意思是不能使用for.它容易和javascript里的for循环混淆，会提示你使用htmlfor。

#### 父组件向子组件传值

父组件向子组件传递内容，靠属性的形式传递。

比如：我们在<Compent>组件中加入content属性，然后给属性传递{item}，这样就完成了父组件向子组件传值。

```js
<Compent content={item} />
```

可以通过this.props.xxx的形式进行接受:

```js
render() { 
    const {content} = this.props;
    return ( 
        <div>{content}</div>
    );
}
```

#### 子组件向父组件传递数据

React有明确规定，子组件时不能操作父组件里的数据的，所以需要借助一个父组件的方法，来修改父组件的内容。

如果子组件要调用父组件方法，其实和传递数据差不多，只要在组件调用时，把方法传递给子组件就可以了,记得这里也要进行this的绑定，如果不绑定子组件是没办法找到这个父组件的方法的。

```js
//父组件中
<ul>
    {
        this.state.list.map((item,index)=>{
            return (
                <XiaojiejieItem 
                key={index+item}  
                //关键代码-------------------start
                deleteItem={this.deleteItem.bind(this)}
                //关键代码-------------------end
                />
            )
        })
    }
</ul>  
```
```js
//子组件中
handleClick(){
    const {deleteItem,index} = this.props;
    deleteItem(index);
}
```
>注意：React的特性中有一个概念叫做“单项数据流”；你只能使用这个值，而不能修改这个值。

#### 函数式编程的好处是什么？

1. 函数式编程让我们的代码更清晰，每个功能都是一个函数。

2. 函数式编程为我们的代码测试代理了极大的方便，更容易实现前端自动化测试。

#### PropTypes校验传递值

安装和导入

```js
//安装 cnpm install --save prop-types

import PropTypes from 'prop-types'
```

在子组件中使用：

```js
// 设置props属性的类型
static propTypes = {
    值1:PropTypes.string,
    值2:PropTypes.func,
    值3:PropTypes.number.isRequired
};
```

#### ref的使用方法

1. 字符串(已废弃)
3. React.createRef() （React16.3提供）


2. 回调函数
如果要使用ref，需要在JSX中进行绑定， 绑定时最好使用ES6语法中的箭头函数，这样可以简洁明了的绑定DOM元素。

```js
<input 
    className="input" 
    //关键代码——----------start
    ref={(input)=>{this.input=input}}
    //关键代码------------end
    />
```

使用：

```js
inputChange(){
    this.setState({
        inputValue:this.input.value
    })
}
```
> ref使用中的坑; 不建议用ref这样操作的，因为React的是数据驱动的，所以用ref会出现各种问题。

因为React中更多setState是一个异步函数所造成的。也就是这个setState，代码执行是有一个时间的；就是因为是异步，还没等虚拟Dom渲染，我们的代码就已经执行了。

其实setState方法提供了一个回调函数，也就是它的第二个函数。下面这样写就可以实现我们想要的方法了。

```js
inputChange(){
    this.setState({
        //...
    //关键代码--------------start
    },()=>{
        inputValue:this.input.value
    })
    //关键代码--------------end
}
```

#### React生命周期图

四个大阶段：

1. Initialization:初始化阶段。

2. Mounting: 挂在阶段。

3. Updation: 更新阶段。

4. Unmounting: 销毁阶段

##### Mounting阶段

Mounting阶段叫挂载阶段，伴随着整个虚拟DOM的生成，它里边有三个小的生命周期函数，分别是：

1. componentWillMount : 在组件即将被挂载到页面的时刻执行。

2. render : 页面state或props发生变化时执行。

3. componentDidMount : 组件挂载完成时被执行。

>componentWillMount和componentDidMount这两个生命周期函数，只在页面刷新时执行一次，而render函数是只要有state和props变化就会执行，这个初学者一定要注意。

##### Updation阶段

组件发生改变的更新阶段，这是React生命周期中比较复杂的一部分，它有两个基本部分组成，一个是props属性改变，一个是state状态改变。

1. shouldComponentUpdate---组件发生改变前执行

2. componentWillUpdate---组件更新前，shouldComponentUpdate函数之后执行

3. render----开始挂载渲染

4. componentDidUpdate----组件更新之后执行

**componentWillReceiveProps 函数**

凡是组件都有生命周期函数，所以子组件也是有的，并且子组件接收了props，这时候函数就可以被执行了。

子组件接收到父组件传递过来的参数，父组件render函数重新被执行，这个生命周期就会被执行。

1. 也就是说这个组件第一次存在于Dom中，函数是不会被执行的;

2. 如果已经存在于Dom中，函数才会被执行。

##### Unmounting阶段

componentWillUnmount，它是在组件去除时执行。

#### React高级-生命周期改善程序性能

通过shouldComponentUpdate函数，改善React组件性能(子组件频繁无用渲染render);

shouldComponentUpdate有两个参数：

1. nextProps:变化后的属性;

2. nextState:变化后的状态;

```js
//完美解决了子组件的渲染性能问题
shouldComponentUpdate(nextProps,nextState){
    if(nextProps.content !== this.props.content){
        return true
    }else{
        return false
    }
   
}
```
