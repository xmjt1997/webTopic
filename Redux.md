

# Redux

### Redux成员

| 成员            | 作用                      | 类型 |
| --------------- | ------------------------- | ---- |
| createStore     | 创建store实例             | 函数 |
| combineReducers | 合并多个reducer           | 函数 |
| applyMiddleware | 安装中间件，改装增强redux | 函数 |

> `⭐`在整个React项目中，store仓库只能定义一个，

### **store成员**

| 成员           | 作用                                           | 类型 |
| -------------- | ---------------------------------------------- | ---- |
| subscribe      | 订阅state变化                                  | 函数 |
| dispatch       | 发送action 给 reducer                          | 函数 |
| getState       | 获取一次state的值                              | 函数 |
| replaceReducer | 一般在 Webpack Code-Splitting 按需加载的时候用 | 函数 |

### **数据流动**

| component（views）      | action              | reducer                                    | state    | component（views）   |
| ----------------------- | ------------------- | ------------------------------------------ | -------- | -------------------- |
| 展示state               | 转发的动作,异步业务 | 同步业务处理逻辑, 修改state，并且返回state | 状态收集 |                      |
| store.dispatch--------> | ------------->      |                                            |          | <--subscribe（订阅） |
|                         |                     |                                            |          | <--getState（获取）  |

### 项目架构

```js
|-src
  |-redux 状态管理
    |-index.js 设置仓库store
    |-reduers.js 设置仓库管理员配置
    |-actionCreators.js 放置action方法 
  	|-actionTypeName.js 放置redux所以action 类型名
    
可用combineReducers方法把reduers.js拆分成多个方法文件。便于区分功能
    
```



### 创建步骤

> index.js

1. 首先从`redux`中导入`createStore ` 
2. 导入`reduers`仓库管理员配置
3. 创建一个`store`仓库，通过`createStore（reduers）`放置`reduers`配置
4. 导出`store`仓库，给react项目使用

```
// store仓库
import { createStore } from 'redux'
import reduers from './reduers'

let store = createStore(reduers)

export default store
```

`⭐`：使用chrome浏览器的调试工具redux，需要在store仓库配置时添加如下方法：

```js
let store = createStore(
    reduers,
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
)
```



> ​	reduers.js

1. 自定义一个默认的defaultState仓库，存放初始数据。
2. let 一个reduers函数，默认传入两个参数（state=default，action）
3. 在reduers函数中写入action方法。
4. 在函数最后返回 state仓库
5. 导出reduers

```js
// reduers管理员

import { } from './actionTpyesName'

// 自定义默认仓库
let defaultState = {
    title: '留言板A',
    list: [],
    inputValue: ''
}

let reduers = (state = defaultState, action) => {

    if (action.type === 'inputvalue') {
        let newState = JSON.parse(JSON.stringify(state))
        newState.inputValue = action.value
        return newState
    }
    if (action.type === 'submitvalue') {
        let newState = JSON.parse(JSON.stringify(state))
        if (newState.inputValue == '') {
            return newState
        }
        else {
            newState.list.unshift(newState.inputValue)
            newState.inputValue = ''
            return newState
        }

    }
    if (action.type === 'deletevalue') {
        let newState = JSON.parse(JSON.stringify(state))
        newState.list.splice(action.index, 1)
        return newState
    }
    
    return state
}

export default reduers
```

`⭐`：在reduers中，仓库state的值不允许直接修改，必须拷贝，更新，返回给仓库进行替换。最后返回修改过拷贝的newState仓库。

> actionTpyesName.js 

​	定义redux管理中用到的action类型名称，便于出错提示和全局管理。

​	用export  const  XXX_XXX = 'xxxx' 命名形势

​	在redux中引入使用

```js
// action type类型常量名定义

export const INPUT_VALUE = 'inputvalue';//更新
export const SUBMIT_VALUE = 'submitvalue';//提交
export const DELETE_VALUE = 'deletevalue'//删除
```



> ​	actionCreators.js

1. 定义一个模块用作书写action请求的类型和传值。
2. 申明一个函数，参数接受组件的传参，
3. let 一个action对象，定义属性 type 和 value，type引用actionTypeName文件中定义好的常量。
4. 引入store仓库，使用 dispatch方法来向reduers来发送请求
5. 批量导出函数方法，供组件调用

```js
// action 对应reduers方法
import { INPUT_VALUE, SUBMIT_VALUE, DELETE_VALUE } from './actionTpyesName'
import store from './index'

export const onInputValue = (e) => {
    let action = {
        type: INPUT_VALUE,
        value: e.target.value,
    }
    store.dispatch(action)
};

……
```



### 响应式渲染

​		react组件要响应式更新数据变化，需要对全局store仓库进行监听，使用store提供的subscribe方法进行订阅，当state里的数据发生变化时候，自动执行回调函数

`一般state订阅不发生在构造器中，可以写在主入口文件 订阅reactdom的更新`

```js
let render = ()=>{
    ReactDOM.render(
      <App/>,
      document.getElementById('root')
    )
};
render();
store.subscribe(render);
```

