---
title: react使用RTKQ配置api
published: 2024-08-10
description: ''
image: ''
tags: [react, store, 本地持久化]
category: '各类问题'
draft: false 
---





# 先配置axios

```typescript
// request.ts
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


// 创建 axiosBaseQuery
const axiosBaseQuery = (
    {baseUrl}: { baseUrl: string } = {baseUrl: ''}
): BaseQueryFn<{
    url: string,
    method: Method,
    data?: object,
    params?: object,
}, unknown, unknown> => async ({url, method, data, params}) => {
    try {
        const response = await instance.request<Data<unknown>>({
            url: baseUrl + url,
            method,
            [method.toUpperCase() === 'GET' ? 'params' : 'data']: method.toUpperCase() === 'GET' ? params : data
        });
        return {data: response.data};
    } catch (axiosError) {
        return {
            error: {axiosError}
        };
    }
};

export default axiosBaseQuery;
```



# 配置例子

```typescript
// src/services/userApi.js
import {createApi} from '@reduxjs/toolkit/query/react';
import axiosBaseQuery from "../configs/request.ts";

export const userApi = createApi({
    reducerPath: 'userApi',
    // 注意替换成axiosBaseQuery
    baseQuery: axiosBaseQuery({ baseUrl: 'https://localhost:8080/api' }),
    endpoints: (builder) => ({
        getUsers: builder.query({
            query: () => ({url: '/users', method: 'GET'}),
        })
    }),
});

export const { useGetUsersQuery } = userApi;
```





# 导出

```typescript
import { configureStore } from '@reduxjs/toolkit';
// @ts-ignore
import { userApi } from './userApi.ts';

export const store = configureStore({
    reducer: {
        [userApi.reducerPath]: userApi.reducer,
    },
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware().concat(userApi.middleware),
});
```

