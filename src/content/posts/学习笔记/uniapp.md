---
title: uniapp 学习笔记
published: 2024-05-20
description: ''
image: ''
tags: [uniapp, 学习笔记]
category: '学习笔记'
draft: false 
---

- [连接雷电模拟器](#连接雷电模拟器)
- [设置底部UI](#设置底部ui)
- [创建分包](#创建分包)
- [条件编译](#条件编译)
- [使用查询器查找结点宽高尺寸](#使用查询器查找结点宽高尺寸)
- [生命周期](#生命周期)
- [封装网络请求](#封装网络请求)
- [封装全局工具函数](#封装全局工具函数)



# 连接雷电模拟器

<img src="https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240422190614.png" alt="QQ截图20240422190614" style="zoom:50%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240422195617.png" alt="QQ截图20240422195617" style="zoom:50%;" />

- 之后运行到APP基座即可。



# 设置底部UI

- `pages.json`中：

```json
// 底部 UI(最少2个最多5个)
    "tabBar": {
        "list": [
            {
                "pagePath":"pages/index/index",
                "text": "首页"
            },
            {
                "pagePath": "pages/index/me",
                "text": "我的"
            }
        ]
    },
```



# 创建分包

- 在根目录下创建分包

<img src="https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240422192226.png" alt="QQ截图20240422192226" style="zoom:50%;" />

- 注意在创建分包文件时，不要在`pages.json`注册

<img src="https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240422192354.png" alt="QQ截图20240422192354" style="zoom:50%;" />



- 在`pages.json`中配置分包

```json
"subPackages": [
        {
            "root": "subpkg",   //分包根目录名
            "pages": [
                {
                    "path": "index/index"   //注册分包下的文件，注意不要写分包名!
                }
            ]
        }
    ],
```



- vue中点击跳转：

```vue
<navigator url="/subpkg/index/index">点击跳转至分包</navigator>
```

**注意最前面要加`/`，要加上分包名**



# 条件编译

```js
// #ifdef

// #endif


// #ifndef

// #endif
```

- **注：既可以用在js，也能用在css，也能用在html**

![QQ截图20240422202350](https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240422202350.png)



# 使用查询器查找结点宽高尺寸

- **注意必须要在生命周期函数中使用**

```vue
<script setup>
    import {onMounted} from 'vue'
    
    onMounted(() => {
        console.log("你好");
        const query = uni.createSelectorQuery();
        query.select('.title').boundingClientRect((res) => {
            console.log(res);
        })
        
        // 必须要执行才有结果
        query.exec();
    })
    
    
</script>
```



# 生命周期

![QQ截图20240423101523](https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240423101523.png)

![QQ截图20240423101608](https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240423101608.png)

![QQ截图20240423101635](https://vip.123pan.cn/1828962653/md-images/uniapp.assets/QQ截图20240423101635.png)



# 封装网络请求

- `cnpm i luch-request`

+ 配置拦截器：

```js
import Request from 'luch-request'

const http = new Request({
    baseURL: 'http://localhost:3000'
    
})

// 配置请求拦截器
http.interceptors.request.use((config) => {
    // config为请求时的所有参数
    
    config.header = {
        // Authorization: '123456',
        ...config.header // 让局部头信息覆盖默认配置
    }
    
    return config;
})

// 响应拦截器
http.interceptors.response.use((config) => {
    const {data} = config;
    console.log(data);
    
    return config;
})

export {http}
```



# 封装全局工具函数

+ `utils.js`：

```js
// 必须要带有uni前缀
uni.utils = {
    toast(title = '加载失败!', icon = 'none'){
        uni.showToast({
            title,
            icon,
            mask: true,   // 防止误触
        })
    }
}
```

+ 导包：在`main.js`中导入包
+ 使用：`uni.utils.toast('你好')`

