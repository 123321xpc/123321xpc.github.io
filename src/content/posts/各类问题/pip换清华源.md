---
title: pip换清华源
published: 2024-05-17
description: ''
image: ''
tags: [python, pip, 各类问题]
category: '各类问题'
draft: false 
---


打开终端或命令行窗口，输入以下命令：
```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

若成功设置，输入以下命令：
```
pip config list
```

能看到如下内容：
```
global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

