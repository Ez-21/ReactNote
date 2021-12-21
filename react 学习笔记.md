> # react 学习笔记

>  #### 1:React 函数组件名`首字母大写 `且必须有返回值

```javascript
function About(){
    return(
    	<span>我是函数组件<span/>
    )
}
```

> ####   2: 函数组件 可以返回`null`

> #### 3: class类组件 必须继承 `React.Component `从而可以使用父类中的方法

> #### 4: 类组件必须提供`render` 方法

```jsx
class Home extends React.Component{
    render(){
        return(
            <div>我是类组件</div>
        )
    }
}
```

> #### 5: 事件的`this`指向

###### 	   第一种：使用箭头函数this返回执行方法

```javascript
onClick={()=>this.edit}
```

###### 	第二种：使用bind()手动指向this

```javascript
1：onClick={this.edit.bind(this)}

2:在实例化中 对函数进行bind 重新赋值 
```

###### 	第三种：class实例this ：原理也是箭头函数的this指向性

```javascript
    edit=()=>{
        do something()
    }
```

> #### 6：使用state 与 修改state

```javascript
`创建state有两种方式`
1：class Meum extends React.Component{
    constructor(){
        this.state = {
            user:{}
        }
    }
}
2:简化写法直接 state = {
    user:{}
}
```

```javascript
`修改state中的数据需要使用 setState()方法`
比如 this.setState({
    user:{
        name:'钱宗泽'
    }
})
```

> #### 7：表单绑定

​	React将state与表单元素的value值绑定在一起，

​	比如`<input type='text' value={this.state.name} onChange={e=>this.change(e)}/>`

```javascript
change=(e)=>{
    this.setState({
        user:{
            name:e.target.value
        }
    })
}
```

> #### 8：组件通讯

​	不管是函数组件、函数类组件 都使用props参数进行接收数据，`警告！！ props是只读对象，不可进行修改！！`

* 1 函数组件 

```jsx
function Box(props){
        return(
            <div>{props.name}</div>
        ) 
}
`传递数据`
<Box name={'林俊杰'}/>
```

* 类组件

```jsx
class Box extends React.Component{
    constructor(props){
        super(props)
        // 在此就可以 直接使用props了
    }
    render(){
        return(
        	<span>{this.props.name}</span>
        )
    }
}
`传递数据`
<Box name={'周杰伦'}/>
```

> #### 9：组件通讯的三种类型

###### 1 父子通讯

```js
`父组件`
class Father extends React.Compenten{
    constructor(){
        super()
        this.state = {
            name:'我是父组件'
        }
    }
    render(){
        return(
        	<Son name={this.state.name}><Son/>
        )
    }
}
`子组件`
function Son(props){
    return(
    	<span>{props.name}</span>
    )
}
```

###### 2 子父通讯

```jsx
`父组件提供一个回调函数`
class Father extends React.Component{
    getMess(sonMess){
        console.log(sonMess,'子组件数据')
    }
    render(){
        return(
        	<div>
            	我是父组件
            	`用什么名称接收，就用什么名称传`
            	<Son `sonGet` = {this.getMess}/>
            </div>
        )
    }
}

`子组件接收父组件回调函数并传值/参`
class Son extends React.Component{
    constructor(props){
       super(props)
        this.state ={
            name:'钱宗泽'
        } 
    }
    btn=()=>{
        this.props.sonGet(this.state.name)
    }
    render(){
        return(
        	<span onClick = {this.btn}>点击我</span>
        )
    }
}
```



###### 3 兄弟通讯

兄弟组件之间的通讯方式 要通过 父组件 作为中间人进行数据传递

即:【老大】=>【爹】=>【老二】

:call_me_hand: 这波啊 这波是懒得写了.....:joy:



> #### 10：嵌套跨组件传值

如果存在多重组件嵌套需要进行传值的情况 则需要使用React.createContext()方法

```jsx
const {Provider,Consumer} = React.creatContext()
class App extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            name:'跨级传递数据'
        }
    }
`使用Provider标签包裹根组件`
    render(){
        return(
            <Provider value={this.state.name}>
            	<One></One>
            </Provider>
        )
    }
}
`使用Consumer接收数据`
function One(props){
    return(
        <Consumer>
        {data=><span>我是{data}</span>}
        </Consumer>
    )
}
```



> #### 11：props的深入

1. ###### props的`children`属性

   ```jsx
   
   function Three(props) {
     console.log(props)
   	return (
   		<div>
   			<Two></Two>
   			<p>three组件</p>
               //接收子节点内容
         		{props.children}
   		</div>
   	);
       
   class mine extends React.Component {
       constructor(props) {
           super(props);
       }
       render() {
           return (
                   <div>
                       <Three>
                      		子节点内容--     
                      	<input type='search' value='我是强行添加的子节点!!' readOnly/>
                       </Three>
                   </div>
           );
       }
   }
   
   ```

2. ###### props的`校验`

   `props的校验允许创建组件的时候就规定props的类型、格式等`

   对于组件来说props是外来数据，我们不知道组件使用者会传递什么类型的数据。

   如果我们组件需要props传递进来的数据不正确 比如：循环时不是数组、使用时不是对象......

   避免这种情况发生 我们需要使用到props的`校验`

   校验类型分为：

   - array、object、func、number、string、bool

   - 必填项：propTypes.number.isRequired

   - React 元素类型 element

   - 特定结构的object对象：shape({})

     

   安装props检验依赖：`npm install props-types -D`

   ```jsx
   Box.propTypes={
       userName = propTypes.object
   }
   ```

   如果数据类型不一致 则：

   ![1639886087850](C:\Users\22758\AppData\Roaming\Typora\typora-user-images\1639886087850.png)

   

3. props的默认值

   ```jsx
   Box.defaultProps = {
   	name:'钱宗泽',
       color:'black'
   }
   ```

 

​	 

> #### 12：组件的生命周期

1. `注意：`只有类组件才有生命周期！
2. 组件具有三种状态生命周期：
3. 1. 创建时
   2. 更新时
   3. 卸载时

- 创建时：顺序分为 1：construtor() ===> 2：render ===> 3：componentDidMount

- |     生命周期      | 触发时机                | 作用                                    |
  | :---------------: | ----------------------- | --------------------------------------- |
  |    constructor    | 创建组件最先执行        | 初始化state，为事件处理程序绑定this指向 |
  |      render       | 每次组件渲染都会被触发  | 渲染页面 `注意:不能调用setState()`      |
  | componentDidMount | 组件挂载，完成DOM渲染后 | 发送网络请求，DOM操作                   |

  更新时：使用setState({})、forceUpdate()、接收到新props时 会执行 render ===> componentUpdate()

  参数：componentUpdate(`prevProps`)代表上一次的props数据
  
  ​	`注意:如果在componentUpdate(prevProps)中使用setState()必须放在一个if条件中判断,否则会造      				成递归更新`
  
  卸载时：componentWillUnmount()
  
  

> #### 13：深入JSX

##### React中的表达式 `以下写法都不会被渲染！！`

![1640084962234](C:\Users\22758\AppData\Roaming\Typora\typora-user-images\1640084962234.png)

##### 可以使用运算符进行判断组件渲染

```jsx
<div>
{cass&&<Hello/>}
</div>
```

