> # `React hooks`

## React中的常用hooks有：

1. ### useState({值})： 在函数组件中设置并使用变量初始值

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

2. ### useEffect(()=>{},['item'])：副作用hook 类似生命周期 

   组件第一次渲染，每次每次更新后都会执行。

   可以声明多个effect React按照顺序执行每一个effect

   React会在组件卸载时执行清除操作

   `清除副作用 ：当Effect 返回一个函数时  effect会在执行清除操作时调用它`

   为了避免每一次组件更新都执行effect,可是为useEffect设置第二个参数：[变量]，只有传入数组中的变量数据发生改变后，才去执行effect

   如果你想只执行一次effect 就传入一个空数组【】，使它仅在加载和卸载时执行

   









