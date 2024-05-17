---
title: mybatis-plus 学习笔记
published: 2024-05-16
description: ''
image: ''
tags: [学习笔记, mybatis-plus]
category: '学习笔记'
draft: false
---

- [引入依赖(Springboot 3.2)](#引入依赖springboot-32)
- [编写配置文件](#编写配置文件)
- [添加mapper](#添加mapper)
- [在启动类中添加注解](#在启动类中添加注解)
- [框架](#框架)
- [基础CRUD](#基础crud)
  - [查询数据](#查询数据)
  - [自定义联表查询](#自定义联表查询)
    - [xml文件方式](#xml文件方式)
  - [添加数据](#添加数据)
  - [删除数据](#删除数据)
  - [修改数据](#修改数据)
- [自定义service接口](#自定义service接口)
- [批量添加数据](#批量添加数据)
- [yml文件配置](#yml文件配置)
- [注解](#注解)
  - [@TableName](#tablename)
  - [@TableId](#tableid)
  - [@TableField](#tablefield)
  - [@TableLogic](#tablelogic)
- [条件构造器wapper](#条件构造器wapper)
  - [搜索`id`以97结尾的数据：](#搜索id以97结尾的数据)
  - [按`id`降序排序：](#按id降序排序)
  - [或条件](#或条件)
  - [优先级](#优先级)
  - [查询特定字段](#查询特定字段)
  - [修改数据](#修改数据-1)
  - [根据条件是否满足组装条件](#根据条件是否满足组装条件)
  - [lamba wapper](#lamba-wapper)
- [分页](#分页)



## 引入依赖(Springboot 3.2)

```xml
		<dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.5</version>
            <exclusions>
                <exclusion>
                    <groupId>org.mybatis</groupId>
                    <artifactId>mybatis-spring</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>3.0.3</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.10</version>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.25</version>
        </dependency>
```



## 编写配置文件

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatisdb?useUnicode=true&characterEncoding=UTF-8
    username: root
    password: aptx4869
    type: com.alibaba.druid.pool.DruidDataSource
#    别名映射
mybatis-plus:
  type-aliases-package: com.example.pojo
```





## 添加mapper

```java
public interface UserMapper extends BaseMapper<User> {
 }
```



## 在启动类中添加注解

```java
@SpringBootApplication
 @MapperScan("com.atguigu.mybatisplus.mapper") //tian'jia
 public class MybatisplusApplication {
 }
```



- `pojo`类：

```java
package com.example.pojo;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Pass {
    private String username, passenger_name, id;
}

```



## 框架

```java
import cn.practice.musicplayer.mapper.MusicMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class MusicService {

    @Autowired
    private MusicMapper musicMapper;

    
}
```





## 基础CRUD

### 查询数据

- 查询所有数据

```java
    public void testPass(){
        List<Pass> passes = passMapper.selectList(null);
        for (Pass pass : passes) {
            System.out.println(pass);
        }
    }
```

- 根据`id`批量查询

```java
public void testPass(){
       List<String> list = new ArrayList<>();
       list.add("2");
       list.add("3");
       list.add("4");
       System.out.println(passMapper.selectBatchIds(list));
    }
```

- 根据少量条件查询

```java
    public void testPass(){
       Map<String, Object> map = new HashMap<>();
       map.put("id", "2");
       map.put("password", "213");
       System.out.println(passMapper.selectByMap(map));
    }
```

###  自定义联表查询

#### xml文件方式

1. 在`resources`目录下创建`mapper`文件夹（名字不能改），后创建mapper.xml文件



### 添加数据

```java
public void testPass(){
    Pass pass = new Pass();
    pass.setPassenger_name("你好");
    pass.setUsername("12321214");
    System.out.println(passMapper.insert(pass));
    
    //获取Id
    System.out.println(pass.getId());
}
```

- **注：`mybatis-plus`会自动默认用雪花算法注入id后插入数据库。**



### 删除数据

- 根据`id`删除

```java
public void testPass(){
        passMapper.deleteById("1754092979703037954");
    }
```

- 少量条件删除

```java
public void testPass(){
        Map<String, Object> map = new HashMap<>();
        map.put("password", "4");
        map.put("username", "123321xx");
        passMapper.deleteByMap(map);
    }


//原理
delete from table where password = '4' and username = '123321xx'
```

- 批量删除

```java
//删除id为1，2，3的数据
public void testPass(){
        List<String> list = new ArrayList<>();
        list.add("1");
        list.add("2");
        list.add("3");
        passMapper.deleteBatchIds(list);
    }
```

- 注意：数据库中的`id`要和`list`的泛型对应。



### 修改数据

```java
    public void testPass(){
        Pass pass = new Pass("1", "2", "333");
        //根据id修改数据
        passMapper.updateById(pass);
    }
```



## 自定义service接口

- `passService`：

```java
public interface PassService extends IService<Pass> {
}
```

- `passServiceImpl`：

```java
@Service
public class PassServiceImpl extends ServiceImpl<PassMapper, Pass> implements PassService {
}

```

- 启动类上增加扫描范围：

```java
@ComponentScan("com.example")
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```

- 测试：

```java
	@Autowired
    private PassService passService;

    @Test
    public void testService(){
        System.out.println(passService.count());
    }
```



## 批量添加数据

```java
public void testService(){
        ArrayList<Pass> list = new ArrayList<>();
        for(int i=1;i<=5;++i)
        {
            Pass pass = new Pass();
            pass.setUsername(i + "");
            pass.setPassword(i+1+"");
            list.add(pass);
        }

        passService.saveBatch(list);
    }
```



## yml文件配置

```yaml
mybatis-plus:
  global-config:
    db-config:
#      设置表的统一前缀
      table-prefix: t_
#      设置全局主键策略(自增)
      id-type: auto
```





## 注解

### @TableName

- 作用：设置实体类的表名

- 例：

```java
@TableName("pass_info")
public class Pass {
    private String username, id, password;
}

```



### @TableId

- 作用：设置主键(当主键名不为id时用)
- 例1：

```java
public class Pass {
    private String username;
    
    @TableId   
    private String uid;  //将uid设为主键
    
    private String password;
}
```

- 例2：value值

```java
public class Pass {
    private String username;

    @TableId(value="pid")
    private String id;  //将id映射到数据库表中的pid，并指定pid为主键

    private String password;
}
```

- 例3：type值

```java
public class Pass {
    private String username;

    @TableId(value="pid", type= IdType.AUTO)  //设置id自增,数据库中必须设置id自增
    private String id;  //将id映射到数据库表中的pid

    private String password;
}
```



### @TableField

- 作用：指定属性对应的字段名
- 例：

```java
public class Pass {
    @TableField("user_name") //将username映射到数据库表中的user_name
    private String userName;

    @TableId(value="pid", type= IdType.AUTO)
    private String id;  //将id映射到数据库表中的pid

    private String password;
}
```



### @TableLogic

- 作用：逻辑删除

```java
public class Pass {
    private String username;

    private String id; 

    private String password;

    @TableLogic
    @TableField("is_deleted")
    private int isDeleted;
}
```

- 在每张表的最后设置一个`is_deleted`字段，类型为`int`，默认值设为0，0表示未删除，1表示已删除。



## 条件构造器wapper

### 搜索`id`以97结尾的数据：

```java
    public void testService(){
        QueryWrapper<Pass> queryWrapper = new QueryWrapper<>();
        queryWrapper.likeLeft("id", "97");
        System.out.println(passMapper.selectList(queryWrapper));
    }
```

### 按`id`降序排序：

```java
    public void testService(){
        QueryWrapper<Pass> queryWrapper = new QueryWrapper<>();
        queryWrapper.orderByDesc("id");
        List<Pass> passes = passMapper.selectList(queryWrapper);
        passes.forEach(System.out::println);
    }
```

### 或条件

```java
    public void testService(){
        QueryWrapper<Pass> queryWrapper = new QueryWrapper<>();
        queryWrapper.gt("id", "1")
                .or() //or表示前面的所有条件和后面的所有条件为或关系
                .lt("id", "0");
        List<Pass> passes = passMapper.selectList(queryWrapper);
        passes.forEach(System.out::println);
    }
```

### 优先级

```java
    public void testService(){
        QueryWrapper<Pass> queryWrapper = new QueryWrapper<>();
        //查询年龄大于20且id小于2，或id为1的用户
        
        //and中的i表示构造器，lamba表达式语句会先执行！
        queryWrapper.gt("id", "1")
                .and(i -> i.gt("age", 20).lt("id", "2"));
        List<Pass> passes = passMapper.selectList(queryWrapper);
        passes.forEach(System.out::println);
    }
```

### 查询特定字段

```java
    public void testService(){
        QueryWrapper<Pass> queryWrapper = new QueryWrapper<>();

        queryWrapper.select("id", "password"); //查询特定字段（其他为null）
        List<Pass> passes = passMapper.selectList(queryWrapper);
        passes.forEach(System.out::println);
    }
```



### 修改数据

![QQ截图20240517224101](/md-images/学习笔记/mybatis-plus.assets/QQ%E6%88%AA%E5%9B%BE20240517224101.png)



### 根据条件是否满足组装条件

![QQ截图20240517224119](/md-images/学习笔记/mybatis-plus.assets/QQ%E6%88%AA%E5%9B%BE20240517224119.png)



### lamba wapper

![QQ截图20240517224135](/md-images/学习笔记/mybatis-plus.assets/QQ%E6%88%AA%E5%9B%BE20240517224135.png)



## 分页

- 配置分页插件

![QQ截图20240517224202](/md-images/学习笔记/mybatis-plus.assets/QQ%E6%88%AA%E5%9B%BE20240517224202.png)

```java
package com.example.interceptor;


import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor;
import com.baomidou.mybatisplus.extension.plugins.inner.PaginationInnerInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class PageInterceptor {
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.MYSQL));
        return interceptor;
    }
}

```

- 使用

```java
   public void testService(){
        Page<Pass> page = new Page<>(2, 3);

        Page<Pass> page1 = passMapper.selectPage(page, null);

        page1.getRecords().forEach(System.out::println);
    }
```

