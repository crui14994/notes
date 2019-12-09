### redux笔记

#### 安装AntDesign

```bash
cnpm install antd --save
```

#### 创建store仓库

```bash
cnpm install --save redux
```

安装好redux之后，在src目录下创建一个store文件夹,然后在文件夹下创建一个index.js文件

```js
import { createStore } from 'redux'  // 引入createStore方法

import reducer from './reducer'

const store = createStore(reducer)          // 创建数据存储仓库
export default store                 //暴露出去          
```

这时候就需要一个有管理能力的模块出现，这就是Reducers;在store文件夹下，新建一个文件reducer.js。

```js
const defaultState = {}  //默认数据
export default (state = defaultState,action)=>{  //就是一个方法函数
    return state
}
```

组件获得store中的数据

```js
import store from './store/index'
```

```js
constructor(props){
    super(props)
    console.log(store.getState())
}
```

#### 安装Redux DevTools

如何配置这个Redux Dev Tools插件

```js
import { createStore } from 'redux'  //  引入createStore方法
import reducer from './reducer'    
const store = createStore(reducer,
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()) // 创建数据存储仓库
export default store   //暴露出去

//其实就是加了这样一句话;
//window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
//这句话的意思就是看window里有没有这个方法，有则执行这个方法
```

#### 创建Action

想改变Redux里边State的值就要创建Action了。Action就是一个对象，这个对象一般有两个属性，第一个是对Action的描述，第二个是要改变的值。

action就创建好了，但是要通过dispatch()方法传递给store。

```js
changeInputValue(e){
    const action ={
        type:'changeInput',
        value:e.target.value
    }
    store.dispatch(action)
}
```

#### store的自动推送策略

store只是一个仓库，它并没有管理能力，它会把接收到的action自动转发给Reducer.

```js
export default (state = defaultState,action)=>{
    console.log(state,action)
    return state
}
// state: 指的是原始仓库里的状态。
// action: 指的是action新传递的状态。
```

改变store里的值。我们先判断type是不是正确的，如果正确，我们需要从新声明一个变量newState。（Reducer里只能接收state，不能改变state。）,所以我们声明了一个新变量，然后再次用return返回回去。

```js
export default (state = defaultState,action)=>{
    if(action.type === 'changeInput'){
        let newState = JSON.parse(JSON.stringify(state)) //深度拷贝state
        newState.inputValue = action.value
        return newState
    }
    return state
}

```

#### 让组件发生更新

写一个storeChange方法；重新setState一次就可以实现组件也是变化的。

```js
 storeChange(){
     this.setState(store.getState())
 }
 ```

 在constructor，写入下面的代码。

 ```js
 constructor(props){
    super(props)
    this.state=store.getState();
    //----------关键代码-----------start
    store.subscribe(()=>this.storeChange()) //订阅Redux的状态
    //----------关键代码-----------end
}
```

#### Redux的小技巧

把Action Types 单度写入一个文件;在src/store文件夹下面，新建立一个actionTypes.js文件，然后把Type集中放到文件中进行管理。

```js
//actionTypes.js
export const  CHANGE_INPUT = 'changeInput'
export const  ADD_ITEM = 'addItem'
export const  DELETE_ITEM = 'deleteItem'
```

引入组件和Reducer中并使用;然后把对应的字符串换成常量

```js
import { CHANGE_INPUT , ADD_ITEM , DELETE_ITEM } from './store/actionTypes'
```

#### 把所有的Redux Action放到一个文件里进行管理

编写actionCreators.js文件；在/src/store文件夹下面，建立一个心的文件actionCreators.js，先在文件中引入上节课编写actionTypes.js文件。

实现Redux Action和业务逻辑的分离，可打打提供程序的可维护性。

```js
//actionCreators.js
import {CHANGE_INPUT}  from './actionTypes'

export const changeInputAction = (value)=>({
    type:CHANGE_INPUT,
    value
})
```

在组件中引入

```js
import {changeInputAction} from './store/actionCreatores'

changeInputValue(e){
    const action = changeInputAction(e.target.value)
    store.dispatch(action)
}
```

#### Redux小坑

1. store必须是唯一的，多个store是坚决不允许，只能有一个store空间

2. 只有store能改变自己的内容，Reducer不能改变

    Reudcer只是返回了更改的数据，但是并没有更改store中的数据，store拿到了Reducer的数据，自己对自己进行了更新。

3. Reducer必须是纯函数

    >纯函数定义：如果函数的调用参数相同，则永远返回相同的结果。它不依赖于程序执行期间函数外部任何状态或数据的变化，必须只依赖于其输入参数。

---

### React-Redux

#### 介绍与安装

React-Redux这是一个React生态中常用组件，它可以简化Redux流程。（需要注意的是概念：React、Redux、React-redux是三个不同的东西）。

安装react-redux：

```js
npm install --save react-redux
```

#### <Provider>提供器讲解

Provider是一个提供器，只要使用了这个组件，组件里边的其它所有组件都可以使用store了，这也是React-redux的核心组件了。

```js
import React from 'react';
import ReactDOM from 'react-dom';
import TodoList from './TodoList'
//---------关键代码--------start
import { Provider } from 'react-redux'
import store from './store'
//声明一个App组件，然后这个组件用Provider进行包裹。
const App = (
   <Provider store={store}>
       <TodoList />
   </Provider>
)
//---------关键代码--------end
ReactDOM.render(App, document.getElementById('root'));
```

#### connect连接器的使用

引入connect，它是一个连接器（其实它就是一个方法），有了这个连接器就可以很容易的获得数据了.

```js
import {connect} from 'react-redux'  //引入连接器
```

这时候暴露出去的就变成了connect了，代码如下。

```js
export default connect(xxx,null)(TodoList);
```

整体案列

```js
import React, { Component } from 'react';
import store from './store'
import {connect} from 'react-redux'

class TodoList extends Component {
    constructor(props){
        super(props)
        this.state = store.getState()
    }
    render() { 
        return (
            <div>
                <div>
                    <input value={this.props.inputValue} />
                    <button>提交</button>
                </div>
                <ul>
                    <li>JSPang</li>
                </ul>
            </div>
            );
    }
}

const stateToProps = (state)=>{
    return {
        inputValue : state.inputValue
    }
}
 
export default connect(stateToProps,null)(TodoList);

```

#### React-redux的数据修改

要使用react-redux，我们可以编写另一个映射DispatchToProps,先看下面这段代码，你会发现有两个参数，第二个参数我们用的是null。

```js
import React, { Component } from 'react';
import store from './store'
import {connect} from 'react-redux'

class TodoList extends Component {
  
    render() { 
        // 集中管理
        let {inputValue ,inputChange} = this.props;

        return (
            <div>
                <div>
                    <input value={inputValue} onChange={inputChange} />
                    <button>提交</button>
                </div>
                <ul>
                    <li>JSPang</li>
                </ul>
            </div>
            );
    }
}
const stateToProps = (state)=>{
    return {
        inputValue : state.inputValue
    }
}

const dispatchToProps = (dispatch) =>{
    return {
        inputChange(e){
            console.log(e.target.value)
        }
    }
}
 
export default connect(stateToProps,dispatchToProps)(TodoList);
```

把TodoList改为UI组件-提高性能

>现在的TodoList组件里没有任何的业务逻辑，只有一个Render方法，这时候就可以把它改为UI组件(无状态组件)，UI组件就是一个方法，减少很多冗余操作，从而提高程序运行性能。

```js
import React from 'react';
import store from './store'
import {connect} from 'react-redux'

const TodoList = (props)=>{
    // 集中管理
    let {inputValue ,inputChange} = this.props;

    return (
        <div>
            <div>
                <input value={inputValue} onChange={inputChange} />
                <button>提交</button>
            </div>
            <ul>
                <li>JSPang</li>
            </ul>
        </div>
    );
}

const stateToProps = (state)=>{
    return {
        inputValue : state.inputValue
    }
}

const dispatchToProps = (dispatch) =>{
    return {
        inputChange(e){
            console.log(e.target.value)
        }
    }
}
 
export default connect(stateToProps,dispatchToProps)(TodoList);
```