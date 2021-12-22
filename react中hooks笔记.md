> # `React hooks`

## React中的常用hooks有：

###useState({值})： 在函数组件中设置并使用变量初始值

##### `注意：setState()设置值 仅作用于 对应的state` 

```jsx
var [state,setState] = useState({
    user:{name:'react-hooks'},
    color:[],
    age:22
})
ck=()=>{
    let {name} = state
    setState({
        name:'钱宗泽'
    })
}
```

![1640080984286](C:\Users\22758\AppData\Roaming\Typora\typora-user-images\1640080984286.png)

### useEffect(()=>{},['item'])：副作用,功能类似生命周期

组件第一次渲染，每次每次更新后都会执行。

可以声明多个effect React按照顺序执行每一个effect

React会在组件卸载时执行清除操作

`清除副作用 ：当Effect 返回一个函数时  effect会在执行清除操作时调用它`

为了避免每一次组件更新都执行effect,可是为useEffect设置第二个参数：[变量]，只有传入数组中的变量数据			发生改变后，才去执行effect

如果你想只执行一次effect 就传入一个空数组【】，使它仅在加载和卸载时执行。

### useMemo(()=>{},['item'])：写法与useEffect相同

传入useMemo中的函数每次组件渲染都会执行，返回值用于保存值 可以用来缓存数据，避免不必要的计算

第二个参数为一个数组，当数组中的元素值发生改变后 触发Memo中的函数。



### useCallback(()=>{},['item'])：写法与useEffect相同

与Memo写法相同 功能相同

与useMemo()不同之处是 `Memo()返回函数值 ` 而`callback()`返回一个回调函数(所以叫callback :happy:)

### useRef()：可以获取Dom元素或者`class`组件实例

```jsx
function App(){
    var ref = React.useRef()
    return(
    	<span ref={ref}></span>
    )
}
```

<img src="C:\Users\22758\AppData\Roaming\Typora\typora-user-images\1640168794004.png" alt="1640168794004"  />

### useLayoutEffect：与Effect()写法相同

不同之处是：layoutEffect比Effect先执行 并且早于浏览器渲染 









