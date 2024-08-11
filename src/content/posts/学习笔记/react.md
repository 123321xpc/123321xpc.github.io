---
 title: react18
published: 2024-06-02
description: ''
image: ''
tags: [学习笔记, react]
category: '学习笔记'
draft: false 

---

- [JSX语法](#jsx语法)
	- [常用JSX语法](#常用jsx语法)
	- [实现列表渲染](#实现列表渲染)
	- [实现基础条件渲染](#实现基础条件渲染)
	- [事件绑定](#事件绑定)
		- [传递自定义参数](#传递自定义参数)
		- [同时传递事件参数和自定义参数](#同时传递事件参数和自定义参数)
- [useState](#usestate)
	- [修改状态的规则](#修改状态的规则)
	- [传递泛型](#传递泛型)
- [组件](#组件)
	- [组件样式](#组件样式)
		- [classnames库](#classnames库)
	- [组件通信](#组件通信)
		- [父传子](#父传子)
			- [children](#children)
		- [子传父](#子传父)
		- [跨层组件](#跨层组件)
- [useEffect](#useeffect)
		- [依赖项](#依赖项)
		- [清除副作用](#清除副作用)
- [hook使用规则](#hook使用规则)
- [Redux](#redux)
	- [配套工具](#配套工具)
	- [store目录结构](#store目录结构)
	- [创建store](#创建store)
	- [注入store](#注入store)
	- [使用store中的数据](#使用store中的数据)
	- [修改store中的数据](#修改store中的数据)
	- [管理异步状态数据](#管理异步状态数据)
- [路由](#路由)
	- [安装](#安装)
	- [路由导航跳转](#路由导航跳转)
	- [声明式导航](#声明式导航)
	- [编程式导航](#编程式导航)
		- [传参](#传参)
	- [嵌套路由](#嵌套路由)
		- [默认二级路由](#默认二级路由)
	- [404路由](#404路由)
	- [2种路由模式](#2种路由模式)
- [useReducer](#usereducer)
- [useMemo](#usememo)
- [React.memo](#reactmemo)
	- [props比较机制](#props比较机制)
- [useCallback](#usecallback)
- [React.forwardRef](#reactforwardref)
- [React.useInperativeHandle](#reactuseinperativehandle)







# JSX语法规则

1. 定义虚拟`DOM`时，不要写引号。

```jsx
const app = <h1>Hello World</h1>
```

1. 样式的类名指定不要用`class`,要用`className`.
2. 内联样式，要用`style={{ key : value }}`的形式去写。

```jsx
<h1 style={{color: "red"}}>Hello World</h1>
```

1. 只有一个根标签
2. 可以使用嵌入式表达式`{}`**（注意与`vue`的插值表达式区别）**

```jsx
const name = 'haha'

<h1>{haha}</h1>
```

6. 标签中混入JS表达式时要用`()`。
	+ `js表达式`：一个表达式会产生一个值，能放在任何一个需要值的地方
		- 如： `a, a + b, func(1), arr.map`等，凡是能用`const x = `接到值的都是表达式
	+ `js语句`：`if, for, switch`

```jsx
function App() {
const arr = [1, 2, 3, 4, 5]
  return (
      <ul>
          {arr.map((item: number) => item + 1)}
      </ul>
  )
}
```



7. 标签必须闭合

8. 标签首字母

	+ 若**小写字母**开头，则将改标签转为`html`中同名元素，若`html`中无该标签对应的同名元素，则报错。

	+ 若**大写字母**开头，`React`就去渲染对应的组件，若组件没有定义，则报错。



> 注：使用`{arr}`，`JSX`会自动将数组的所有元素依次打印出来



## 常用JSX语法

![202406031519905](https://vip.123pan.cn/1828962653/md-images/202406031519905.png)



## 实现列表渲染

![202406031519852](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031519852.png)

## 实现基础条件渲染

![202406031520587](https://vip.123pan.cn/1828962653/md-images/202406031520587.png)



## 事件绑定

![202406031520992](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520992.png)



### 传递自定义参数

![202406031520289](https://vip.123pan.cn/1828962653/md-images/202406031520289.png)



### 同时传递事件参数和自定义参数

![202406031520435](https://vip.123pan.cn/1828962653/md-images/202406031520435.png)



![202406031520102](https://vip.123pan.cn/1828962653/md-images/202406031520102.png)







# React三大核心API







# state

+ `state` 是一个对象，用于存储组件级别的动态数据。
+ **特点**:
	- **本地性**: `state` 是组件私有的，其他组件不能直接访问或修改另一个组件的 `state`。
	- **动态性**: 当 `state` 发生变化时，React 会自动重新渲染组件，以反映最新的 `state`。
+ **注意：只有值被修改时，才会重新渲染。**

下述情况页面不会重新渲染，因为对象没变

```jsx
function App() {
    const [user, setCount] = useState({name: '小米'})
    
    const updateUser = () => {
        user.name = '小红'
        setCount(user)
        // setCount({...user}) 这样会重新渲染，对象改变
    }
    
    return (
      <div>
          <h1>{user.name}</h1>
          <button onClick={() => updateUser()}>+</button>
      </div>
  )
}
```







> 直接修改变量无法在页面显示的原因：`html`元素先渲染，当函数执行时，值修改了，但页面不会重新渲染，所以页面看不到更新结果。



## useState

![image-20240609192018714](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192018714.png)

> + 注意
>
> 	1. **使用新的对象替换原对象**
> 	2. **函数是异步的**，所以当短时间重复执行，并且**需要用到原state值时**，可能会计算错误, 此时需要使用回调函数的形式
>
> 	```jsx
> 	 const updateCount = () => {
> 	     setCount(count + 1)
> 								
> 	     // 换成如下方式，React会确保先更新完上一次的state，再更新下一次的state
> 	     setCount(prevVal => prevVal + 1)
> 	}
> 	```
> 	
> 	3. 必须将`setState()`放入函数中使用，不能直接放入最外层函数体中。
> 	
> 	如下代码：
> 	
> 	```jsx
> 	function App() {
> 	    const [count, setCount] = useState(0)
> 	    setCount(count + 1)
> 	    return (
> 	      <>
> 	          <h1>{count}</h1>
> 	          <button onClick={() => console.log("Increment")}>Increment</button>
> 	      </>
> 	    )
> 	}
> 	```
> 	
> 	会报如下错误：
> 	
> 	![image-20240802231243127](https://vip.123pan.cn/1828962653/md-images/image-20240802231243127.png)
> 	
> 	原理：
> 	
> 	+ 当`setState()`被调用时，会先判断此时处于哪个阶段
> 	
> 		+ 若不是渲染阶段，则执行常规检查。对象相同则不渲染，不同则渲染。
> 			+ 当组件中存在子组件时，**若修改对象不涉及到子组件**，则当父组件第一次修改的对象相同时，还是会重新渲染一遍，但**子组件不会重新渲染**，若第二次修改对象没变，则父组件也不会再渲染。
> 	
> 		```jsx
> 		function App() {
> 		    console.log('App component rendered')
> 		    const [count, setCount] = useState(0)
> 		    return (
> 		      <>
> 		          <h1>{count}</h1>
> 		          <Child />
> 		          <button onClick={() => setCount(1)}>Increment</button>
> 		      </>
> 		    )
> 		}
> 		```
> 	
> 		如上代码：当点击按钮2次时，打印输出如下：
> 	
> 		![image-20240802232146068](https://vip.123pan.cn/1828962653/md-images/image-20240802232146068.png)
> 	
> 		当第三次点击时，父子组件均不会渲染。
> 	
> 		
> 	
> 		+ **若是渲染阶段，则不会检查，直接重新渲染。导致一致重复渲染**
> 	
> 			





## 修改状态的规则

![image-20240609192430656](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192430656.png)

![image-20240609192551509](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192551509.png)



## 传递泛型

![image-20240610154311431](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610154311431.png)



![image-20240610154726394](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610154726394.png)



# Ref & useRef

+ 获取原生DOM元素

```jsx
	const r1 = useRef(null)
   
   	return (
      <div>
          <h1 ref={r1}>{count}</h1>
          <button onClick={updateCount}>+</button>
      </div>
    )
```

+ ### `useRef` 的特点

	1. **可变 `current` 属性**:

	  - `useRef` 返回的对象是一个有`current` 属性的对象，初始值为传递给 `useRef` 的参数。

	  - `current` 是可变的，你可以随时更改它，而不会导致组件重新渲染。

	  - 也就是说，不一定非要使用`useRef`钩子，如下代码照样能拿到原生DOM元素

	  - ```
	
	  	const r1 = 
	  	```
	
	  - 二者区别：
	
	  	- `useRef` 返回的对象在组件的整个生命周期内保持不变，即 `ref` 对象在每次渲染时都是相同的。
	
	3. **无渲染影响**:
	
		- 更新 `.current` 的值不会导致组件的重新渲染，这是 `useRef` 的一个关键特性，适用于需要持久化但不需要触发渲染的场景。

# 组件

## 组件样式

![image-20240609192834816](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192834816.png)



> 注：
>
> 1. 多个单词必须用小驼峰。
> 2. 是`className`，不是`class`



### classnames库

![image-20240609193706313](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609193706313.png)



## 组件通信

### 父传子

- 父组件传递数据

![image-20240609193952490](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609193952490.png)

- 子组件接收数据

![image-20240609194024452](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194024452.png)

- 说明：

![image-20240609194139934](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194139934.png)

#### children

![image-20240609194601080](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194601080.png)



### 子传父

![image-20240609194709092](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194709092.png)



### 跨层组件

![image-20240609200105423](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200105423.png)

1. 

![image-20240609195404529](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195404529.png)

2. 

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195523677.png" alt="image-20240609195523677" style="zoom:67%;" />

3. 

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195436584.png" alt="image-20240609195436584" style="zoom: 80%;" />



# useEffect

## 什么是副作用？

在 React 中，**副作用通常涉及与组件渲染过程无关的操作**。

1. **数据获取**: 发送`AJAX`。
2. **DOM 操作**: 手动修改 DOM，比如操作非受控组件的值。
3. **本地存储**: 读取或写入浏览器的本地存储（`localStorage / sessionStorage`）。



+ 这些操作在页面渲染阶段执行会影响页面渲染，进而影响性能。
	+ 例如：
		+ 在渲染阶段调用`setState()`会报错`to many render`
		+ 执行打印语句会使页面重新渲染一次



## useEffect清除副作用原理

1. `useEffect` 可以返回一个函数，这个函数会在组件卸载或者副作用需要重新执行之前调用。页面渲染时不会调用。这就是清除副作用的过程。返回的这个函数被称为清理函数或清除函数。
2. 清理函数的调用时机
	1. **组件卸载时**:
		- 当组件被从 DOM 中移除时，React 会调用 `useEffect` 的清理函数。这是确保在组件生命周期结束时，所有的副作用都被正确清除。
	2. **依赖项更新时**:
		- 如果 `useEffect` 的依赖数组（第二个参数）中的某个依赖项发生了变化，React 会在执行新的副作用之前调用上一次执行 `useEffect` 时返回的清理函数。这是为了确保在同一个组件实例中更新副作用时，前一个副作用得到正确的清理。
	3. **重新渲染时（在某些情况下）**:
		- 在没有依赖数组的情况下，每次组件渲染都会执行 `useEffect`，因此每次都会执行清理函数。虽然通常不推荐这样使用，但这是可能的行为。



## 使用

![image-20240609200439554](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200439554.png)

### 依赖项

![image-20240609200919404](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200919404.png)

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201148661.png" alt="image-20240609201148661" style="zoom:50%;" />

>上述代码，每当count改变时，函数就会执行。
>
>`setState()`没有必要写进去，因为`useState`会保证获取到的`setState`是同一个对象。



### 清除副作用

![image-20240609201324456](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201324456.png)

 例：

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201718375.png" alt="image-20240609201718375" style="zoom:50%;" />



# hook使用规则

![image-20240609202538548](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609202538548.png)

# Redux

## 配套工具 RTK

**Redux Toolkit (RTK)** 旨在简化Redux应用程序的配置和操作。它包括几个核心部分：

- **`configureStore`**：简化了store配置过程，自动添加了一些通常需要手动设置的中间件，如 `Redux Thunk`。
- **`createReducer`** 和 **`createSlice`**：这些API简化了`reducer`的创建过程，允许以更声明性的方式定义`reducers`和`actions`。
- **`createAsyncThunk`**：用于处理异步逻辑，而无需编写大量的`action creators`和处理每个请求状态的`action`。
- **`createEntityAdapter`**：自带的可直接使用的`CRUD`

**RTK Query (RTKQ)** 是`Redux Toolkit`的一部分，专门用于处理数据获取和缓存的需求。主要特点包括：

- **自动数据缓存**：数据请求后自动缓存，减少不必要的网络请求。
- **数据获取钩子**：如 `useQuery` 和 `useMutation`，这些`React Hook`允许组件直接与`API`数据交互。
- **轻松的数据更新**：`RTK Query`管理响应和缓存，支持乐观更新和无效化技术，使得数据始终保持最新。

![image-20240609203827967](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609203827967.png)



## 使用RTKQ

### 第一步：设置 API 服务

首先，我们创建一个 RTK Query API slice 来定义数据获取的逻辑。

```tsx
// src/api/apiSlice.ts
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

type User {
  id: number;
  name: string;
  email: string;
}

export const apiSlice = createApi({
  reducerPath: 'api',
  baseQuery: fetchBaseQuery({ baseUrl: 'https://jsonplaceholder.typicode.com/' }),
  endpoints: (builder) => ({
    getUsers: builder.query<User[], void>({
      query: () => 'users'
    })
  })
});

export const { useGetUsersQuery } = apiSlice;
```

这段代码定义了一个 `User` 类型和一个 `getUsers` 查询，用来获取用户列表。

### 第二步：在组件中使用 `useQuery` 钩子

接下来，创建一个 React 组件来使用 `useGetUsersQuery` 钩子。

```tsx
typescript复制代码// src/components/Users.tsx
import React from 'react';
import { useGetUsersQuery } from '../api/apiSlice';

const Users: React.FC = () => {
  const { data: users, error, isLoading } = useGetUsersQuery();

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <div>
      <h1>Users</h1>
      <ul>
        {users?.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
};

export default Users;
```

### 第三步：配置 Redux Store

配置 Redux store 并添加我们的 API slice。

```typescript
typescript复制代码// src/app/store.ts
import { configureStore } from '@reduxjs/toolkit';
import { apiSlice } from '../api/apiSlice';

export const store = configureStore({
  reducer: {
    [apiSlice.reducerPath]: apiSlice.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(apiSlice.middleware),
});
```

### 第四步：提供 Redux Store

最后，在应用的入口文件中包装你的应用组件，以便提供 Redux store。

```tsx
typescript复制代码// src/index.tsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { store } from './app/store';
import Users from './components/Users';

ReactDOM.render(
  <Provider store={store}>
    <Users />
  </Provider>,
  document.getElementById('root')
);
```



### 将`fetchBaseQuery`换成`axios`

```typescript
import axios, {type Method} from 'axios';
import {BaseQueryFn} from '@reduxjs/toolkit/query';

// 创建 axios 实例
const instance = axios.create({
    baseURL: 'https://localhost:8080/',
    timeout: 10000
});


// 定义接口返回数据类型
type Data<T> = {
    code: number;
    message: string;
    data: T;
}

// 封装请求方法
export const request = <T>(url: string, method: Method = 'GET', data?: object) => {
    return instance.request<never, Data<T>>({
        url,
        method,
        // 动态属性
        [method.toUpperCase() === 'GET' ? 'params' : 'data']: data
    })
}


export const axiosBaseQuery = (
): BaseQueryFn<
    { url: string; method?: Method; data?: object },
    unknown,
    unknown
> => async ({url, data, method = 'GET'}) => {
    try {
        const result = await instance.request({
            url: url,
            method,
            [method.toUpperCase() === 'GET' ? 'params' : 'data']: data
        });
        return {data: result.data};
    } catch (axiosError) {
        return {
            error: {axiosError},
        };
    }
};

export default axiosBaseQuery;
```







## 本地持久化插件 redux-persist





# 路由

## 安装

```
cnpm i react-router-dom
```



## 路由导航跳转

## 声明式导航

![image-20240610144035333](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144035333.png)

## 编程式导航

![image-20240610144117422](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144117422.png)

### 传参

![image-20240610144554126](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144554126.png)

- 注意：`Param`传参必须要在路由文件中写明键值

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144935140.png" alt="image-20240610144935140" style="zoom:50%;" />



## 嵌套路由

![image-20240610145100434](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145100434.png)

### 默认二级路由

![image-20240610145656203](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145656203.png)

## 404路由

![image-20240610145800181](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145800181.png)



## 2种路由模式

![image-20240610150024633](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610150024633.png)



# useReducer

+ **为了避免页面渲染时反复创建`reducer`函数，一般将之创建在函数体外面。**

![image-20240610150400129](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610150400129.png)



![image-20240610151032828](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151032828.png)

# useMemo

![image-20240610151332204](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151332204.png)



# React.memo

![image-20240610151735143](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151735143.png)

![image-20240610151803008](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151803008.png)

## props比较机制

![image-20240610152158813](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152158813.png)

> 当传递的是复杂数据时，比较的是引用是否变化。而当组件重新渲染时，引用会改变！

+ 若需要保证渲染过程中复杂数据的引用不变，可以对数据使用useMemo，如下：

![image-20240610152632237](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152632237.png)



# useCallback

+ `useCallback`创建的函数不会总在组件渲染时重新创建，只会在依赖数组元素发生变化时重新创建
+ 传入`[]`表示函数只在初始化时创建。

![image-20240610152802414](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152802414.png)

# React.forwardRef

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153235460.png" alt="image-20240610153235460" style="zoom: 33%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153258190.png" alt="image-20240610153258190" style="zoom:33%;" />



# React.useInperativeHandle

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153413782.png" alt="image-20240610153413782" style="zoom:33%;" />

+ 子组件：

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153538540.png" alt="image-20240610153538540" style="zoom:50%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153655032.png" alt="image-20240610153655032" style="zoom:50%;" />