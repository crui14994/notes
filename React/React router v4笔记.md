## React router v4笔记

### 基础知识

使用npm来进行安装

```js
npm install --save react-router react-router-dom
```

#### ReactRouter动态传值

1. 设置, 以:开始的，然后紧跟着你传递的key（键名称）名称。

    ```js
    <Route path="/list/:id" component={List} />
    ```

2. Link上传递值

    ```js
    <li><Link to="/list/123">列表</Link> </li>
    ```

    to属性的值可以是一个字符串，也可以是一个location（pathname, hash, state和search）对象。

3. 组件上接收并显示传递值

    ```js
    componentDidMount(){
        console.log(this.props.match)
    }
    ```
    然后在浏览器的控制台中可以看到打印出的对象，对象包括三个部分:

    - patch:自己定义的路由规则，可以清楚的看到是可以产地id参数的。

    - url: 真实的访问路径，这上面可以清楚的看到传递过来的参数是什么。

    - params：传递过来的参数，key和value值。

#### 理解和使用Route

Route组件可以使用如下的属性：

- path属性，字符串类型，它的值就是用来匹配url的。

- component属性，它的值是一个组件。在path匹配成功之后会绘制这个组件。

- exact属性，这个属性用来指明这个路由是不是排他的匹配。

- strict属性， 这个属性指明路径只匹配以斜线结尾的路径。

    还有其他的一些属性，可以用来代替component属性。

- render属性，一个返回React组件的方法。传说中的rencer-prop就是从这里来的。

- children属性，返回一个React组件的方法。只不过这个总是会绘制，即使没有匹配的路径的时候

    数的时候是用component属性就可以满足。但是，某些情况下你不得不使用render或children属性。

#### ReactRouter重定向-Redirect使用

1. 标签式重定向

    这个一般用在不是很复杂的业务逻辑中，比如我们进入Index组件，然后Index组件,直接重定向到Home组件。

    ```js
    //引入Redirect
    import { Link , Redirect } from "react-router-dom";
    
    //引入Redirect后，直接在render函数里使用就可以了
    <Redirect to="/home/" />
    ```
2. 编程式重定向

    ```js
    //直接在构造函数constructor中加入下面的重定向代码
    this.props.history.push("/home/");  
    ```

---

### 进阶

#### React router的Route中component和render属性的使用

1. component ---只有当位置匹配时才会渲染的 React 组件

    当您使用 component（而不是 render 或 children ）Route 使用从给定组件 React.createElement 创建新的 React element。这意味着，如果您为 component 道具提供了内联功能，则每次渲染都会创建一个新组件。这会导致现有组件卸载和安装新组件，而不是仅更新现有组件。当使用内联函数进行内联渲染时，使用 render 或者 children（如下所示）

2. render: func ---这允许方便的内联渲染和包裹，而不是上面那种不想要的重新安装的解释

    您可以传递一个在位置匹配时调用的函数，而不是使用属性为您创建新的 React element component，该 render 属性接收所有相同的 route props 的 component 渲染属性。

    > 警告： Route component 优先于 Route render 因此不要在同一个 Route 使用两者。

通过一个小例子来说明：

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {BrowserRouter, Route} from "react-router-dom";

class Bar extends React.Component {

    componentDidMount() {
        console.log("componentDidMount")
    }

    render() {
        return (
            <div>Bar</div>
        )
    }
}

class App extends React.Component {

    constructor(prop) {
        super(prop);
        this.state = {idx: 1}
    }

    handleClick = () => {
        this.setState(state => ({idx: state.idx + 1}))
    };

    render() {
        return (
            <div>
                <div>
                    {this.state.idx}
                    <button onClick={this.handleClick}>add</button>
                </div>
                <div>
                    <BrowserRouter>
                        <Route component={Bar}/>
                    </BrowserRouter>
                </div>
            </div>
        );
    }
}


ReactDOM.render(<App/>, document.getElementById('root'));

//上面的代码中，App组件内有一个简单的Bar组件，通过component属性被Route引用。
//<Route component={Bar}/>
//此时在页面中点击按钮，Bar组件的componentDidMount并不会被触发。
```
假设现在需要在Bar组件中接受App中的idx，需要将idx作为props传递给Bar，此时可以写成如下代码

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {BrowserRouter, Route} from "react-router-dom";

class Bar extends React.Component {

    componentDidMount() {
        console.log("componentDidMount")
    }

    render() {
        const {idx} = this.props;
        return (
            <div>in Bar : {idx}</div>
        )
    }
}

class App extends React.Component {

    constructor(prop) {
        super(prop);
        this.state = {idx: 1}
    }

    handleClick = () => {
        this.setState(state => ({idx: state.idx + 1}))
    };

    render() {
        return (
            <div>
                <div>
                    {this.state.idx}
                    <button onClick={this.handleClick}>add</button>
                </div>
                <div>
                    <BrowserRouter>
                        <Route component={() => (<Bar idx={this.state.idx}/>)}/>
                    </BrowserRouter>
                </div>
            </div>
        );
    }
}


ReactDOM.render(<App/>, document.getElementById('root'));
```
然而此时点击按钮，发现Bar的componentDidMount一直被调用，所以正确的写法应该是:

```js
<Route render={() => (<Bar idx={this.state.idx}/>)}/>
//此时Bar组件就不会出现重复的unmounting和mounting了。
```

其背后的原理在于，react在比较组件状态以便决定如何更新dom节点时，首先要比较组件的type和key。在使用<Route component={() => (<Bar idx={this.state.idx}/>)}/>时，由于调用了React.createElement，组件的type不是Bar这个类，而是一个匿名函数。App组件每次render时都生成一个新的匿名函数，导致生成的组件的type总是不相同，所以会产生重复的unmounting和mounting。


#### react路由懒加载（异步组件）------react-loadable

> [npm地址](https://www.npmjs.com/package/react-loadable)

1. 安装

    ```bash
    cnpm install react-loadable
    ```

2. 封装loadable

    首先，我们建一个util    src/util/loadable.js

    ```js
    import React from 'react';
    import Loadable from 'react-loadable';

    //通用的过场组件
    const loadingComponent =()=>{
        return (
            <div>loading</div>
        ) 
    }

    //过场组件默认采用通用的，若传入了loading，则采用传入的过场组件
    export default (loader,loading = loadingComponent)=>{
        return Loadable({
            loader,
            loading
        });
    }
    ```

3. 调用

    ```js
    import loadable from '../util/loadable'

    const Home = loadable(()=>import('@pages/home'))
    ```
    react-loadable是以组件级别来分割代码的，这意味着，我们不仅可以根据路由按需加载，还可以根据组件按需加载。



---

### 参考

[React Router 印记中文](https://react-router.docschina.org/)

[React Router 使用教程](https://juejin.im/post/5d88a2e7f265da03cf7accd5#heading-9)

[利用react-router4的react-router-config做路由鉴权](https://segmentfault.com/a/1190000015282620)


