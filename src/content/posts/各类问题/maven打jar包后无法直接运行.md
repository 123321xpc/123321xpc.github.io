---
title: maven打jar包后无法直接运行
published: 2024-07-13
description: ''
image: ''
tags: [maven]
category: '各类问题'
draft: false 
---





使用`maven`打`jar`包后，无法直接用`java -jar`命令运行`jar`包，终端显示**没有主清单属性**



解决方法：将打包插件中的`Configuration`坐标删去即可

```xml
			<plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>${spring-boot.version}</version>
<!--                <configuration>-->
<!--                    <mainClass>cn.practice.usercenterserver.UserCenterServerApplication</mainClass>-->
<!--                    <skip>true</skip>-->
<!--                </configuration>-->
                <executions>
                    <execution>
                        <id>repackage</id>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

